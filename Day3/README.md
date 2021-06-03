### Invoking setup module to gather facts about the ansible node
```
ansible -i hosts ubuntu1 -m setup
```

### Invoking ad-hoc command when the ansible.cfg file points to the inventory file
```
ansible ubuntu1 -m setup
ansible ubuntu -m setup
ansible centos -m setup
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
As you have noticed, the each additional v adds additional level of verbosity for debugging/troubleshooting purposes.
For Unix/Linux you may try upto 4 levels of verbosity and the 5th level is meant for Windows ansible node.
