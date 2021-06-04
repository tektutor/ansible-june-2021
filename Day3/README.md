### Invoking setup module to gather facts about the ansible node
```
ansible -i hosts ubuntu1 -m setup
```

### Invoking ad-hoc command when the ansible.cfg file points to the inventory file
```
ansible ubuntu1 -m setup
ansible ubuntu -m setup
ansible centos -m setup
ansible all -m ping
ansible all -m shell -a "hostname -i"
```
In the above commands, 'ubuntu1' is an individual ansible node, whereas 'ubuntu' and 'centos' are group of ansible nodes.

### Executing Playbook
```
ansible-playbook -i hosts ping.yml
```

### Executing Playbook in the presence of ansible.cfg that points to inventory file
```
ansible-playbook ping.yml
```

### You may enable the verbosity optionally
```
ansible-playbook ping.yml -v
ansible-playbook ping.yml -vv
ansible-playbook ping.yml -vvv
ansible-playbook ping.yml -vvvv
```
As you have noticed, each additional 'v' adds additional level of verbosity for debugging/troubleshooting purposes.
For Unix/Linux you may try upto 4 levels of verbosity and the 5th level is meant for Windows ansible node.  Anything more than 5 'v's are simply ignored by Ansible :)


### You may now access the nginx web pages
```
curl http://172.17.0.2:80
curl http://172.17.0.3
```
The assuption is 172.17.0.2 and 172.17.0.3 are the IP Addresses of your ubuntu containers. This may be different in your system.
