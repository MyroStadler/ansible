# Ansible

## Vault password file

You will only need the vault password if you need to run anything with encrypted variables that look like `!vault | ...` in it. This should not be a problem since encrypted variables would always be inventory files and you would always create and run your own inventory files.

The `.vault_password` file you might create from the `.vault_password.dist` file (the .dist file serves no purpose other than to remind one that a password should be here) must contain only the master ansible vault password, no newlines or whitespace.
**You must ensure the .vault_password file is NEVER committed to git!**

Specify this file's location in your `~/.ansible.cfg` (see section "Example ~/.ansible.cfg") 

## Local content

Git will ignore any folders that start with `.local`. You can put anything you like in these, like your own inventory files that contain the host and variables for a standard playbook so you can call e.g. `ansible-playbook some-play-in-repo.yml -i .local/my-personal-inventory.yml`.

Note that since files in `.local*` folders are never checked in to the repo you can put plaintext passwords in them without having to use Ansible's vault, very usefult for making your own inventories.

## Git access
 
Best practice for authentication with git servers is to use SSH keys, so playbooks are built to use the SSH protocol for git.
Servers should preserve the auth socket if you want SSH agent forwarding to work so your local SSH identity is passed along for git clone etc.; 
have this line in `/etc/sudoers`:
```bash
Defaults        env_keep+=SSH_AUTH_SOCK
``` 

Three things are needed for you to be able to run playbooks that check out public repos:

1. You must have your [local machine] identity's public key on the git repo's server
1. You must configure ansible to forward SSH identities (see section "Example ~/.ansible.cfg")
1. You must `ssh-add` your identity [on your local machine] so ssh-agent has something to forward

NOTE: if the repo is private (discouraged, you should FLOSS every day) you will need to be a collaborator or have your public key added as a deploy key for the repo.

## Example `~/.ansible.cfg`

```
[defaults]
vault_password_file = ~/.ansible/.vault_password
transport = ssh
remote_tmp = /tmp/${USER}/ansible

[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=60s -o ControlPath=/tmp/ansible-ssh-%h-%p-%r -o ForwardAgent=yes -o ConnectTimeout=16
retries = 5
timeout = 16
pipelining = True
control_path = /tmp/ansible-ssh-%%h-%%p-%%r
```

## SSL and security certificate files

The strategy for SSL certs is to first install with a default snake oil cert, then use certbot to set up a real cert 
and replace the cert values in the vhost file.
