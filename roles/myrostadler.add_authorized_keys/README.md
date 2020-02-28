Add Authorized Keys
===================

Add lines to the remote user's `~/.ssh/authorized_keys` file.

Requirements
------------

None

Role Variables
--------------

add_authorized_keys[]

Dependencies
------------

None

Example Playbook
----------------

```
---
- name: Add authorized keys to remote user
  hosts: all
  become: true
  vars:
    add_authorized_keys: 
      - foo
      - bar
  tasks:
  - include_role: 
      name: myrostadler.add_authorized_keys
```

License
-------

GPL-3.0-only

Author Information
------------------

Myro Stadler
