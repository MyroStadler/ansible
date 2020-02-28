Remove Authorized Keys
======================

Remove lines from the remote user's `~/.ssh/authorized_keys` file.

Requirements
------------

None

Role Variables
--------------

remove_authorized_keys[]

Dependencies
------------

None

Example Playbook
----------------

```
---
- name: Remove authorized keys from remote user
  hosts: all
  become: true
  vars:
    remove_authorized_keys: 
      - foo
      - bar
  tasks:
  - include_role: 
      name: myrostadler.remove_authorized_keys
```

License
-------

GPL-3.0-only

Author Information
------------------

Myro Stadler
