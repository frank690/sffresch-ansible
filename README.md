### sffresch-ansible
I use this repository to provision some of my private servers.
Read the explanation of the different roles below to learn what role should be used to do what.

#### Available roles

| Role | State | Description |
| ---- | ---- | ---- |
| user-setup | Ready | Use to setup one to n sudo users. |
| ufw | Ready | Setup firewall rules. |
| pip | Ready | Install pip3 and some packages. |
| ghost | In Progress | Install [ghost blog](https://ghost.org/) and its requirements.|

#### How to run it
Clone the repo to the environment that ansible should be run from (controlling node).
Setup configurations (see ansible.cfg and the variables in each vars/main.yml of the roles you want to run/use).
An hosts-file should be present containing the target machines (target nodes). 
This file contains the ip addresses of the target nodes as well as further informations/variables (if necessary). 
It can be generated manually or via terraform script. 
If you have different ssh keys for machines - specify it with `ansible_ssh_private_key_file` as in example below.

```sh
[hosts]
192.168.0.123
127.0.0.1

[hosts:var]
variable1=30

[other-hosts]
8.8.8.8 ansible_ssh_private_key_file=~/.ssh/not-default-ssh-key.pem
```

The main.yml (main ansible script file) should be configured according to the hosts file (or other way around). 
Pay attention to which role is executed on which host. 
This is determined by the "hosts" variable in the main.yml and the [section] in the hosts file.
Finally, open a terminal and run the ansible script via:

```python
ansible-playbook main.yml -i hostsfile -t "roles,that,should,be,used"
```