# ansible_php8_centos9
Ansible deployment for php 8 on Centos 9

This is intended to whip up a dev php stack on Centos 9
- Installs mysql. installs conf file, doesnt do anything more with mysql
- Installs php8
- Creates self signed certificate
- Install nginx, default config that has no server blocks
- Installs nginx conf for example site, https only redirect to https

Example usage: ansible-playbook -i ansible/hosts/dev ansible/playbooks/site.yml

Files to modify for project

group_vars/prod
- For each admin that will have sudo access to server
- use the pasted command to generate the sudo password
- key is the name of the pubkey file. Generate a private/pubkey for your user, copy the key into the keys directory
- ip, this field is used in the nginx config to redirect to https. Update script to use site name for production

roles/server_init/files/hosts
- Not required on one node setups, fill out with each node used if in multiple (i.e multiple web servers or a db server on a different node)

roles/site_isntall/templates/example.conf
- This used the ip field from earlier to redirect http to https
