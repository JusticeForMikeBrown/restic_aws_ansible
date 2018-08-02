
Deploy Restic Backups in S3 using Ansible
=======================

This role will deploy Restic backup client in S3 using Ansible

Message that role ran will be sent to Slack as will status of backups.  Failure will also be sent via email

Requirements
------------

You must have Ansible 2.0 installed.

You need a Slack server

CentOS 6 or 7

Examples
--------

To run the role

```
ansible-playbook restic.yml -e hosts=host --sudo -K --ask-vault-pass
```

Notes
--------
The role will by default backup all filesystems on a server only excluding those as defined in var ***restic_exclude.***

I handle this using the following example in ***group_vars/all***:

```
restic_exclude:
- /dev
- /media
- /mnt
- /nfs
- /proc
- /run
- /sys
- /cgroup
- /tmp
- /var/tmp
- /media
- /lost+found
- /srv
- /selinux
- /homes*/*.cache
- /home/*/.cache
- /home/.cache
- /home/*/.local
- /home/*/.gvfs
- /gpfs
```

You must configure lifecycle policies in AWS which **only** migrate the "data" folder to Glacier otherwise restic will stop working.

You should be encrypting ***vars.yml*** using ***ansible-vault***.
