[![Build Status](https://travis-ci.org/ralphie02/ansible-ufw.svg?branch=master)](https://travis-ci.org/ralphie02/ansible-ufw)

ansible-ufw
=========

A basic role to install ufw and rules indicated in the defaults folder.

Requirements
------------

The role needs the variables set correctly on a separate file indicating the port, name, interface and optional from * to IP addresses. Please see example in `Role Variables` below.

Role Variables
--------------
```
fw_direction: in
fw_rule: allow
fw_proto: tcp
```
based on the defaults above, the firewall rule in `sample01.yml` indicated below will allow tcp in via port 22 or if the ip corresponds with the values below.

sample01.yml
```
fw:
  sample01:
    - { port: 22, name: sample01 | Allow port 22  }
    - { from_ip 192.128.128.24, to_ip: 192.128.128.25, name: sample01 | Allow from and to IP }
```

Rule `sample02.yml` on the other hand, allows incoming tcp connection via port 44

sample02.yml
```
fw:
  sample02:
    - { port: 44, name: sample02 | Allow port 44  }
```

Note that the key for the rule values should correspond to the filename; ie. `sample01` <--> `sample01.yml`

Example Playbook
----------------
```
- hosts: server1
  roles:
     - { role: firewall, vars: { fw_list: [sample01] } }

- hosts: server2
  roles:
     - { role: firewall, vars: { fw_list: [sample01, sample02] } }
```
