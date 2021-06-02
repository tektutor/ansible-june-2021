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

### Building Custom Ansible Node Docker Images

#### You need to generate ssh keys as regular user(non-admin)
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
```
docker build -t tektutor/ansible-ubuntu ubuntu-ansible
docker build -t tektutor/ansible-centos centos-ansible
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
