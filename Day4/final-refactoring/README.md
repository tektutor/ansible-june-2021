### Executing the playbook
```
ansible-playbook install-nginx-playbook.yml
```

### Limiting the playbook exeuction to particular machine or group of machines without modifying playbook
```
ansible-playbook install-nginx-playbook.yml --limit centos1
ansible-playbook install-nginx-playbook.yml --limit ubuntu1,centos1
```
