## Setting up your Ansible Controller Machine

### Installing Docker in CentOS
```
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce
sudo systemctl enable docker
sudo usermod -aG docker jegan
sudo su jegan
```
You need to edit /usr/lib/systemd/system/docker.service as shown below 
```
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock -H tcp://0.0.0.0:4243
```
You need to restart docker service as shown below
```
systemctl daemon-reload
systemctl restart docker
```
### Installing Python 3.8.3
```
sudo yum -y update
sudo yum -y groupinstall "Development Tools"
sudo yum -y install openssl-devel bzip2-devel libffi-devel zlib-devel
sudo yum -y install wget
wget https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz
tar xvf Python-3.8.3.tgz
cd Python-3.8*/
./configure --enable-optimizations
sudo make install
```

### Configuring python 3.8.3 as default
```
sudo update-alternatives --config python
```
Choose the serial number under which Python 3.8.3 is listed.

### Install Ansible
```
sudo python -m pip install ansible-core
ansible --version
```

## Building Custom Ansible Node Docker Images

### You need to generate ssh keys as regular user(non-admin)
```
ssh-keygen
```
Accept all defaults by hitting Enter key.

The generated public key of that user must be copied into ubuntu-ansible and centos-ansible folders as shown below
```
cd ansible-june-2021/Day2/ansible-docker-images
cp /home/jegan/.ssh/id_rsa.pub ubuntu-ansible/authorized_keys
cp /home/jegan/.ssh/id_rsa.pub centos-ansible/authorized_keys
```

### Building Ansible Ubuntu Docker Image
The assumption is you are under ansible-june-2021/Day2/ansible-docker-images folder.
```
docker build -t tektutor/ansible-ubuntu ubuntu-ansible 
docker build -t tektutor/ansible-centos centos-ansible
```

### Creating containers
```
docker run -d --name ubuntu1 --hostname ubuntu1 -p 2001:22 -p 8001:80 tektutor/ansible-ubuntu:latest
docker run -d --name ubuntu2 --hostname ubuntu2 -p 2002:22 -p 8002:80 tektutor/ansible-ubuntu:latest
docker run -d --name centos1 --hostname centos1 -p 2003:22 -p 8003:80 tektutor/ansible-centos:latest
docker run -d --name centos2 --hostname centos2 -p 2004:22 -p 8004:80 tektutor/ansible-centos:latest
```

### Testing ssh connection to the above containers
```
ssh -p 2001 root@localhost
ssh -p 2002 root@localhost
ssh -p 2003 root@localhost
ssh -p 2004 root@localhost
```

### Creating static inventory file, you may name it as hosts
```
[all]
ubuntu1 ansible_user=root ansible_host=localhost ansible_port=2001 ansible_private_key_file=/root/.ssh/id_rsa
ubuntu2 ansible_user=root ansible_host=localhost ansible_port=2002 ansible_private_key_file=/root/.ssh/id_rsa
centos1 ansible_user=root ansible_host=localhost ansible_port=2003 ansible_private_key_file=/root/.ssh/id_rsa
centos2 ansible_user=root ansible_host=localhost ansible_port=2004 ansible_private_key_file=/root/.ssh/id_rsa

[ubuntu]
ubuntu[1:2]

[centos]
centos[1:2]

```

### Ansible ad-hoc 
```
ansible -i hosts all -m ping
ansible -i hosts ubuntu1 -m ping -vvvv
ansible -i hosts ubuntu -m ping
ansible -i hosts centos -m ping
```


### What happens when you run the below command
```
ansible -i hosts ubuntu1 -m ping
```

1. First ansible will do an ssh to the ansible node "ubuntu1" using the details given in hosts inventory file.
2. Ansible creates a temporary folder in ACM and Ansible node
3. Ansible uses sftp/scp to copy the ping.py ansible module from ACM tmp to Ansible node tmp folder
4. Ansible executes the copied ping.py on the Ansible Node and captures the output
5. Ansible removes the tmp folder created locally in ACM and the Ansible Node
6. Prints a summary of output in the ACM
