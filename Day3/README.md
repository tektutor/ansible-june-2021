### Invoking setup module to gather facts about the ansible node
```
ansible -i hosts ubuntu1 -m setup
```

### Invoking adhco command when the ansible.cfg file points to the inventory file
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
