# A collection of Ansible playbooks

Here lies a personal collection of Ansible notebooks. I mostly use these notebooks to turn a fresh Debian install into a home media server, a Gitea server, or any other kind of server. On rare occasions, I turn to some of these scripts to update and upgrade all of my machines if a vulnerability requires a fast update on all of my servers. These scripts work on my machine but will probably not run on yours without some minor tweaking. If you want to run any of them, I highly recommend using the command:

```
ansible-playbook Playbooks/YourPlaybookHere -i Inventory/Inventory.yml --ask-vault-pass --limit=group1,group2,host1,host2
```

## Folder structure

This is the folder structure that this repository will always try to follow:

- **Inventory**:  This part of the repository will not be shared, but if you copy this repository, I highly recommend you use `ansible-vault`. 
- **Playbooks**
    - Playbook 1
    - Playbook 2
    - ...
    - Docker:
        - Docker_Images: Contains all of the docker composes I use in some of my scripts.
        - Docker_Config: I will not be sharing my config files, so some of the docker composes may not work out of the box. If this is the case, you may comment that part of the playbook or enter your own docker config file in that folder.


## Available Ansible playbooks

### SecurityPatch.yml

Simple and small playbook that copies the user's local key and pastes it in the remote server. After that the playbook disables SHH login via password.

### SetUp_GiteaServer.yml

As the name implies, after running the same script as `SecurityPatch.yml` it will create a Gitea server and a VPN to connect to it.

### SetUp_HomeServer.yml

This script is special to me, it runs every service I run in my homelab. With this script I try to create a declarative system (Like NixOS) for all of the services I run, so if anything were to happen to my homeserver, I would just need to run this script and copy all of my previous programs and data to the new server.

This script will be modified as I add/remove services to my homelab but I will try to preserve the docker composes.

### SetUp_Wireguard.yml

As the name implies, after running the same script as `SecurityPatch.yml` it will create a server with a WireguardVPN VPN installed in it.

### UpdateUpgrade.yml

Updates and upgrades all of the targeted servers.



