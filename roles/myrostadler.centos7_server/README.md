Centos7 Server
==============

Install server packages.

Requirements
------------

none

Role Variables
--------------

All variables are defaulted in `defaults/main.yml`.

Dependencies
------------

none

Example Playbook
----------------

```
---
- name: "Install server packages"
  hosts: all
  become: true
  tasks:
    - include_role:
        name: myrostadler.centos7_server
```

License
-------

GPL-3.0-only

Author Information
------------------

Myro Stadler
