# IAC with Ansible


## Install Ansible and tree
- `sudo apt-add-repository`
- `sudo apt install ansible tree`


## Configure agent nodes for Ansible

configure each agent node by adding them in `/etc/ansible/hosts` like this:
```
[web]
192.168.33.10 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant

[db]
192.168.33.11 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
```

test the connection by pinging them `ansible all -m ping`

copy host file to agent `ansible web -m copy -a "src=/etc/ansible/README.md dest=/home/vagrant/README.md"`

test file has been copied `ansible web -a 'ls'`


## [Ansible Playbooks](sync/Playbooks)
playbooks are reusable yaml/yml script files to implement config management. (filename.yaml/yml)

### Playbook syntax

#### Playbook header
```
---
# Add name of Host/IP/group
- hosts: web
# Collect logs
  gather_facts: yes
# sudo or not?
  become: true
  tasks
  - name: task name here
    task:
      arg:
      arg2:
```

#### Tasks
- `apt` apt package manager, `pkg` to define package, `state=present` to set the package to running, `update_cache: yes` for updating package list and  `upgrade: yes` to upgrade packages.
- `copy` to copy files to agent/s, `src` for source, `dest` for destination and `force: yes` for forcing overwriting.
- `service` similar to `systemctl`, `name` to define service name, `state=restarted` to restart service, `enabled=yes` to enable service.
- `shell` to run shell commands, separated by a comma.
- `lineinfile` to edit a text file, `path` to define file path, use `line` to append, use `regexp` and `insertafter` in conjuntion to `line` to replace text.




