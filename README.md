# proxmox-upgrade
This playbook automates the upgrade process for [Proxmox Virtual Environment](https://www.proxmox.com/en/proxmox-ve) (PVE) and [Proxmox Backup Server](https://www.proxmox.com/en/proxmox-backup-server) (PBS).

Currently following upgrade paths are supported:
* Proxmox Virtual Environment version `7->8`
* Proxmox Backup Server version `2->3`

This playbooks follows the instructions from the offical documentation:
* [Proxmox Virtual Environment Upgrade from 7 to 8](https://pve.proxmox.com/wiki/Upgrade_from_7_to_8)
* [Proxmox Backup Server Upgrade from 2 to 3](https://pbs.proxmox.com/wiki/index.php/Upgrade_from_2_to_3)

This is a work in progress, if you find any bugs or problems please open a new issue.

## details of PVE upgrade:
* check prerequisites
* create backup of important configuration files under `/var/backups`
* install latest packages from current version
* shutdown virtual maschines
* Debian dist-upgrade
* reboot

I highly recommend running the `pve7to8 --full` checklist tool first and fix all detected problems before upgrading.

You should also use it after the upgrade to verify that everything is ok.

## details of PBS upgrade:
* check prerequisites
* create backup of important configuration files under `/var/backups`
* install latest packages from current version
* put datastores in read-only mode
* Debian dist-upgrade
* reboot
* put datastores back in write mode
* check needed services

## playbook usage

  1. install this playbook via Ansible Galaxy
  ```
  ansible-galaxy install marvhh.proxmox_upgrade
  ```
  2. create a playbook yaml file

example:
```yaml
- name: Upgrade proxmox server
  become: true
  hosts: proxmox_server

  roles:
    - marvhh.proxmox_upgrade
```
  4. run ansible-playbook 

## Options

Following [options](defaults/main.yml) are currently supported:
* `reboot`: Choose if the reboot of the maschine should be done automatically
* `shutdown_vms`: shutdown virtual maschines automatically
* `use_enterprise_repos`: should the [Proxmox enterprise repositories](https://pve.proxmox.com/wiki/Package_Repositories) be used?

## TODO

- [x] Documentation
- [x] put data storages in list and iterate them
- [x] check if PBS Version 2.x is high enough for upgrade
- [ ] list files to edit after upgrade find /etc -name "*.dpkg-dist"

## Author

[Marvin Stark](https://github.com/marvhh)
