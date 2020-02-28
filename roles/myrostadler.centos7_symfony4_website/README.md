Centos7, Symfony4 Website
==========================

Install a Symfony4 website from a git repo on Centos7.

Requirements
------------

Apache with SSL, PHP >= 7, git and MariaDB / PostgreSQL.

Role Variables
--------------

### Has default value

Please see `defaults/main.yml` for defaults.

### Has no default value

- install_env_database_name
- install_env_database_user
- install_env_database_password
- install_env_database_root_password
- install_env_app_secret
- install_dir_name
- install_repo_ssh_uri


Dependencies
------------

- geerlingguy.composer

Example Playbook
----------------

```
---
- name: Install a Symfony4 website from a git repo on Centos7
  hosts: all
  become: true
  vars:
    install_env_database_name: fizizzle_dev
    install_env_database_root_password: foo
    install_env_database_user: bar
    install_env_database_password: baz
    install_env_app_secret: superSecretKeyTellNoone
    install_dir_name: fizizzle
    install_repo_ssh_uri: git@git.example.com:username/repo.git
  tasks:
  - include_role: 
      name: myrostadler.centos7_symfony4_website
```

License
-------

GPL-3.0-only

Author Information
------------------

Myro Stadler