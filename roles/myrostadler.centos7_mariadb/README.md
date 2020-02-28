Centos7, MariaDB
================

Install MariaDB on Centos7.

Requirements
------------

none

Role Variables
--------------

- env_database_root_password
- env_database_user
- env_database_password

Dependencies
------------

none

Example Playbook
----------------

```
---
- name: Install MariaDB on Centos7
  hosts: all
  become: true
  vars:
    env_database_root_password: foo
    env_database_user: bar
    env_database_password: baz
  tasks:
  - include_role: 
      name: myrostadler.centos7_mariadb
```

License
-------

GPL-3.0-only

Author Information
------------------

Myro Stadler