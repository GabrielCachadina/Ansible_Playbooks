# A collection of Ansible playbooks

Here lies a personal collection of Ansible playbooks. I mostly use these notebooks to turn a fresh Debian install into a home media server, a Gitea server, or any other kind of server. On rare occasions, I turn to some of these scripts to update and upgrade all of my machines if a vulnerability requires a fast update on all of my servers. These scripts work on my machine but will probably not run on yours without some minor tweaking. If you want to run any of them, I highly recommend using the command:

```bash
ansible-playbook Playbooks/Playbookhere -i Inventory/Inventory.yml --ask-vault-pass --limit=group1,group2
```

## Folder structure

This is the folder structure that this repository will always try to follow:

- **Inventory**:  This part of the repository will not be shared, but if you copy this repository, I highly recommend you use `ansible-vault`. I follow this structure:
```
[raspi]
192.168.0.xx ansible_user=user_name_here ansible_ssh_pass=password_here ansible_become_pass=password_here
```
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

### SetUp_3dPrintingServer.yml

This playbook installs and boots an [OctoPrint](https://octoprint.org/) docker container.


### SetUp_Computer.yml

Sets up a copy of my computer into another computer, copying the dot-files, nixos-config and all of my important files.


### SetUp_GiteaServer.yml

This playbook will create a [Gitea](https://about.gitea.com/) server. Note that this does not use `https` so it is recommended to use a VPN or to tunnel the traffic with the following command:

```bash
ssh -f -N -L 3000:localhost:3000 root@xx.xx.xx.xx
```
Note that gives any user that can tunnel to have root access, a possible TODO would be to create an unprivileged user that is used only to tunnel traffic.

### SetUp_HomeServer.yml

This script is special to me, it runs every service I run in my homelab. With this script I try to create a declarative system (Like NixOS) for all of the services I run, so if anything were to happen to my homeserver, I would just need to run this script and copy all of my previous programs and data to the new server.

This script will be modified as I add/remove services to my homelab but I will try to preserve the docker composes.

### SetUp_MachineLearningServer.yml

After installing the security patch, it installs a container running [Jupyter notebook](https://jupyter.org/) and another running [Tensorboard](https://www.tensorflow.org/tensorboard). Note that Tensorboard must run the minimum requirements to run. The default token I setup for Jupyterlab is `token`.

### SetUp_PrintingServer.yml

This playbook will create a server the [cups](https://openprinting.github.io/cups/cups3.html) utility installed.

### Setup_StreamlitApp

This playbook sets up a streamlit app and gets it ready to activate the `venv` and deploy the app in port `80`


### SetUp_Website.yml

This playbook will create a server that hosts a website. After it runs it is recommended to run `certbot --nginx` to configure https. A possible TODO would be to create a `cronjob` to automate the certbot script.

### SetUp_Wikipedia.yml

Sets up a [Wiki.js](https://js.wiki/) instance in the targeted machine. 

### SetUp_Wireguard.yml

As the name implies, after running the same script as `SecurityPatch.yml` it will create a server with a [WireguardVPN](https://www.wireguard.com/) VPN installed in it.

### StopAll_DockerContainers.yml

This notebook stops all docker containers running in the target machine.

### UpdateUpgrade.yml

Updates and upgrades all of the targeted servers.

## Aditional notes

Any playbook not listed above is problaly been tested and thus, will probably not work.


