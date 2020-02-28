Certbot
=======

Install certbot and replace cert paths in vhost.

Requirements
------------

A working apache installation on Centos7, with a target virtualhost file (see below). 

Your virtualhost file, pointed to by the variable ``,` must have the `SSLCertificateFile (...)` and `SSLCertificateKeyFile (...)` lines,
otherwise there is nothing to replace with the actual cert file names. Note that the search pattern has a space after the key name, so be sure to include a space.

Role Variables
--------------

All variables are defaulted in `defaults/main.yml`.

Dependencies
------------

- geerlingguy.certbot -- you should definitely override the variables it uses: https://galaxy.ansible.com/geerlingguy/certbot

Example Playbook
----------------

```
---
- name: Install certbot and replace cert paths in vhost
  hosts: all
  become: true
  vars:
    install_dir_name: fizizzle
    
    # geerlingguy.certbot 
    certbot_auto_renew: true
    certbot_create_if_missing: true
    certbot_create_method: standalone
    certbot_admin_email: info@example.com
    certbot_certs:
      - domains:
          - "{{ inventory_hostname }}"
    certbot_create_standalone_stop_services:
      - httpd

  tasks:
  - include_role: 
      name: myrostadler.certbot
    vars:
```

License
-------

GPL-3.0-only

Author Information
------------------

Myro Stadler
