# Ansible Playbook for full automated Proxmox Backup Server Upgrades

This playbook upgrades Proxmox Backup Server 2.x to 3.x following the [official introduction](https://pbs.proxmox.com/wiki/index.php/Upgrade_from_2_to_3).

This is a work in progress, there is still work to do and some comfort functions missing documentation.

## usage

  1. Clone this repository to your local drive.
  2. include it in your roles folder
  3. create a playbook yaml file

```yaml
- name: Upgrade Proxmox Backup Server
  become: true
  hosts: all

  roles:
    - pbs-upgrade
```
  4. run ansible-playbook 
  
## TODO
- [ ] Documentation
- [ ] put data storages in list and iterate them
- [ ] check if PBS Version 2.x is high enough for upgrade

## Author

[Marvin Stark](https://github.com/marvhh), 2023
