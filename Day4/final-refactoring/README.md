### Executing the playbook
```
ansible-playbook install-nginx-playbook.yml
```

### Limiting the playbook exeuction to particular machine or group of machines without modifying playbook
```
ansible-playbook install-nginx-playbook.yml --limit centos1
ansible-playbook install-nginx-playbook.yml --limit ubuntu1,centos1
```

### Fixing the pip3 ssl error
```
python -m pip install --upgrade pip
```

### Installing Python Docker SDK to use docker_container and docker_image ansible modules
```
pip3 install docker
```
