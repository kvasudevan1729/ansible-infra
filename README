# Overview

This repository contains ansible manifests for provisioning 
proxmox and related artifacts.

## Setup

Instructions to install Ansible is outlined here: https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html

To setup roles, please run ansible-galaxy. For e.g, to install the ansible 
docker role, run
```
ansible-galaxy role install geerlingguy.docker
```

### Ansible Vault

Passwords are encrypted using Ansible Vault. Populate the `ansible_vault` file 
with password, and then invoke `ansible-vault`:

```
cd ansible
ansible-vault encrypt_string --stdin-name 'secret_name' --vault-password-file vault_pass
Reading plaintext input from stdin. (ctrl-d to end input, twice if your content does not already have a newline)
My.Vault.Secret
Encryption successful
secret_name: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          64656337666637333637643066323339666136316233613163353930303331336361363965663134
          6133376336313736623833353136323137643666653262630a616537373464326538313438623039
          35373839613532386537353935313338646233316264313530353134343934303230356331643937
          3138646432343163610a313938323964666134613132323865353734646236666262376137333062
          6530
```

`--stdin-name` will prompt for password, and `secret_name` is the variable name. 
Press ctrl-d twice to exit the vault session.

To encrypt a file run:
```
ansible-vault encrypt <file to encrypt> --vault-password-file vault_pass
```

### Ansible Playbook

To run a playbook:
```
cd ansible
ansible-playbook -i inventory.yml playbooks/proxmox-ve/main.yml --vault-password-file vault_pass
```

To run a specific task within a playbook, for instance to configure the 
Grafana alloy agent on the proxmox node for site `lab`, run:
```
ansible-playbook -i inventory.yml playbooks/proxmox-ve/alloy.yml \
   -e "@sites/lab.yaml" --limit "lab-pve01"  --vault-password-file vault_pass -v
```

The `sites/lab.yml` provides the site specific values, and we limit the host to 
the master node `lab-pve01`.
