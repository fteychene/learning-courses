+++
title = "Basic"
description = "Ansible - Basics"
date = 2025-05-01T08:00:00+00:00
updated = 2021-05-01T08:00:00+00:00
draft = false
sort_by = "weight"
weight = 420
template = "ansible/page.html"

[extra]
toc = true
top = false
+++

## Welcome inventories

Ansible works against multiple systems in your infrastructure at the same time. It does this by selecting portions of systems listed in Ansible’s inventory, which defaults to being saved in the location `/etc/ansible/hosts`. You can specify a different inventory file using the -i <path> option on the command line.

To work on your new configured VM, add it's ip to the ansible inventory file `/etc/ansible/hosts`
```bash
echo 192.168.0.2 >> /etc/ansible/hosts
```

By doing this you add your VM to the global inventory of ansible in the all group (if you don't have already some groupe configured in this file ...).

You can test the connection to your VM with the ansible command, using the `ping` module.  
```bash
ansible all -u vagrant -m ping 
```
The `-u` option define the suer to connect with on the VM.  
Th `-m` define the module to be executed on VMs from the all group

## Connection user

If you would like to access sudo mode, there are also flags to do that:

```bash
# as bruce
$ ansible all -m ping -u bruce
# as bruce, sudoing to root
$ ansible all -m ping -u bruce -b
# as bruce, sudoing to batman
$ ansible all -m ping -u bruce -b --become-user batman
```
(The sudo implementation is changeable in Ansible’s configuration file if you happen to want to use a sudo replacement. Flags passed to sudo (like -H) can also be set there.)


## Ad-hoc commands

Now run a live command on all of your nodes:
```bash
$ ansible all -u vagrant -a "/bin/echo hello"
```

Congratulations! You’ve just contacted your nodes with Ansible.  
It’s soon going to be time to: 

* read about some more real-world cases in Introduction To Ad-Hoc Commands
* explore what you can do with different modules
* learn about the Ansible Working With Playbooks language. Ansible is not just about running commands, it also has powerful configuration management and deployment features. 

There’s more to explore, but you already have a fully working infrastructure!

## Exercice

Start multiple VMs and configure ansible to run `hostname` to all your VM with one command