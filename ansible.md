### CLI

$ ansible all -m setup
$ ansible web -m ping
$ ansible web -a /bin/date
$ ansible web -m command -a date

$ ansible-playbook -i inventory.yaml <playbook>.yml -l workers

$ ansible-doc yum --> help for yum module
$ ansible-doc -l --> list modules

### Modules

$ ansible web -m shell -a 'echo $TERM'

$ ansible web -m copy -a "src=/srv/servers.txt dest=/tmp/servers.txt"

$ ansible web -m file -a "dest=/tmp/test/{data-{0,1,2}} mode=777 owner=root group=root state=directory"

$ ansible node1 -m yum -a "name=screen state=latest" -b
$ ansible node1 -m yum -a "name=kubectl-1.16.0-4 state=present"
$ ansible node1 -m yum -a "name=kubectl state=latest"
$ ansible node1 -m yum -a "name=kubectl state=absent"

$ ansible web -m service -a "name=httpd state=restarted"

$ ansible node1 -m command -a 'rpm -qi httpd' --> verify it's installed
$ ansible all -m setup -a filter=*hostname*

### Become

```
# as bruce
$ ansible all -m ping -u bruce
# as bruce, sudoing to root (sudo is default method)
$ ansible all -m ping -u bruce --become
# as bruce, sudoing to batman
$ ansible all -m ping -u bruce --become --become-user batman
```

### /etc/sudoers

ansible ALL=(ALL) NOPASSWD: ALL

### Ansible

- playbook
- modules
- plugins
- inventory --> where ansible deploys
- CLI

$ ls -la ~.ansible.cfg

### Inventory

- flat file, have multiple groups

$ cat /home/student<X>/lab_inventory/hosts

$ ansible-inventory -y --list  --> current inventory
$ ansible-inventory -i inventoru --list  --> current inventory

### Ping a Group


$ ansible web -m ping
$ ansible web -m command -a "uptime"

### Listing Modules

$ ansible-doc -l | grep yum
$ ansible-doc yum --> get help for yum module

- script* module --> execute on a remote host

### `command` Module

$ ansible node1 -m command -a "id"
$ ansible all -m command -a 'uname -r'
$ ansible node1 -m yum -a "name=screen state=latest" -b

### `copy` Module

$ ansible node1 -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd'
$ ansible node1 -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd' -b

$ ansible node1 -m command -a 'cat /etc/motd' - check work

### Running a Playbook

$ ansible-playbook --syntax-check playbooks/apache.yml
$ ansible-playbook --check playbooks/apache.yml

$ ansible-playbook apache.yaml
$ ansible-playbook playbook-name.retry --> contains list of hosts where it failed use with --limit
$ ansible-playbook --ask-become-pass or -K --> ask for a password

$ ansible-playbook -i production site.yml --tags ntp --> configure NTP on everything
$ ansible-playbook -i production site.yml -t ntp --> configure NTP on everything
$ ansible-playbook -i production site.yml --tags ntp,secondTag --> run 2 tags
$ ansible-playbook -i production webservers.yml --tags ntp --list-tasks --> list NTP tasks
$ ansible-playbook -i production webservers.yml --skip-tags ntp --> skip tags

### An Ansible Play

- hosts
- connection
- port
- remote user
- become
- name --> identifier
- roles
- tasks
- handlers
- gather_facts
- check_mode --> dry run

### Variables

```
Here comes a variable {{ variable1 }}
```

$ ansible-playbook -i inv web.yml -e "target_service=httpd"
$ ansible-playbook <playbook> -e @vars.yaml

### Ansible Facts

$ ansible node1 -m setup
$ ansible node1 -m setup -a 'filter=ansible_eth0'
$ ansible node1 -m setup -a 'filter=ansible_*_mb'

$ ansible node1 -m setup -a 'filter=ansible_distribution'  -o

$ ansible-playbook facts.yaml

### Conditionals

### Handlers

- make an additional tasks after a change has been done (e.g. restart service after config change)
- The “notify” section calls the handler only when the copy task actually changes the file. That way the service is only restarted if needed - and not each time the playbook is run

### Simple Loops

### Loop Over Hashes

- The `user` module has the optional parameter `groups` to list additional users. To reference items in a hash, the `keyword needs to reference the subkey:` for example.

### Templates

- When a template for a file has been created, it can be deployed to the managed hosts using the template module, which supports the transfer of a local file from the control node to the managed hosts

### Roles

- While it is possible to write a playbook in one file, eventually you’ll want to reuse files and start to organize things.

- Ansible Roles are the way we do this. When you create a role, you deconstruct your playbook into parts and those parts sit in a directory structure.

$ ansible-galaxy

$ ansible-galaxy init --offline roles/apache_vhost

### Ansible Tower

- multiple teams
- role-based access control
- logging
- workflows

https://student31.workshopname.rhdemo.io

ssh student31@student31.0329.rhdemo.io

### A Tower Project

- A Tower Project is a logical collection of Ansible Playbooks. You can manage your playbooks by placing them into a source code management (SCM) system supported by Tower, including Git, Subversion, and Mercurial.

### Add Tempalte Survey

- The survey feature only provides a simple query for data - it does not support four-eye principles, queries based on dynamic data or nested menus.

### Ansible Tower Workflow

- Workflows were introduced as a major new feature in Ansible Tower 3.1. The basic idea of a workflow is to link multiple Job Templates together. They may or may not share inventory, Playbooks or even permissions. The links can be conditional

### Ansible Vault

$ ansible-vault decyprt <file>
$ ansible-vault encrypt <file>
$ ansible-vault encrypt --vault-id label@prompt <file>
$ ansible-vault view <file>
$ ansible-vault edit <file>
$ ansible-vault encrypt_string --vailt-id prod@prompt 'new_var: new-value'