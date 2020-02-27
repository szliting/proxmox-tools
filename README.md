# ProxmoxTools
📦 A collection of stuff that I wrote for Proxmox 📦

[![GitHub Release][releases-shield]][releases]
[![License][license-shield]](LICENSE.md)

![Project Maintenance][maintenance-shield]
[![GitHub Activity][commits-shield]][commits]
[![Discord][discord-shield]][discord]
![Community Forum][forum-shield]

[![Twitter][twitter]][twitter]
[![Github][github]][github]

<!-- 🎉 Release of ProxmoxTools 0.0.1 -->

## About

# Proxmox tools
This is a collection of usefull stuff for Proxmox.

## Proxmox config backup

I just wrote this script quick and dirty. Not really tested yet! But it might still be of help.
Example:
-<--->-

### Features

-<--->-
<!-- also includes... -->


### Backup
* Download the [script](https://raw.githubusercontent.com/marrobHD/proxmox-tools/master/prox_config_backup.sh)  
```cd /root/; wget -qO- https://raw.githubusercontent.com/marrobHD/proxmox-tools/master/prox_config_backup.sh```
* Set the permanent backups directory ```export BACKUP_DIR="/path/to/backup/directory"```
* Make the script executable ```chmod +x ./prox_config_backup.sh```
* Shut down ALL VMs + LXC Containers if you want to go the save way. (Not required) ```service pve-manager stop```
* Run the script ```./prox_config_backup.sh```

### Restore
On my machine, you end up with a GZipped file of about 1-10 MB with a name like "proxmox_backup_proxmoxhostname_2017-12-02.15.48.10.tar.gz".  
Depending upon how you schedule it and the size of your server, that could eventually become a space issue so don't  
forget to set up some kind of archive maintenance.

To restore, move the file back to proxmox with cp, scp, webmin, a thumb drive, whatever.  
I place it back into the /var/tmp directory from where it came. 

```
# Unpack the original backup
tar -zxvf proxmox_backup_proxmoxhostname_2017-12-02.15.48.10.tar.gz
# unpack the tared contents
tar -xvf proxmoxpve.2017-12-02.15.48.10.tar
tar -xvf proxmoxetc.2017-12-02.15.48.10.tar
tar -xvf proxmoxroot.2017-12-02.15.48.10.tar

# If the services are running, stop them:
for i in pve-cluster pvedaemon vz qemu-server; do systemctl stop $i ; done

# Copy the old content to the original directory:
cp -avr /var/tmp/var/tmp/etc/* /etc/
cp -avr /var/tmp/var/tmp/var/* /var/
cp -avr /var/tmp/var/tmp/root/* /root/


# And, finally, restart services:
for i in qemu-server vz pvedaemon pve-cluster; do systemctl start $i ; done
```

If nothing goes wrong, and you have separately restored the VM images using the default ProxMox process.  
You should be back where you started. But let's hope it never comes to that.

### Sources
http://ziemecki.net/content/proxmox-config-backups



FEEL FREE TO POST ISSUES


## Authors & contributors

The original setup of this repository is by [Marlon][TechHome].

For a full list of all authors and contributors,
check [the contributor's page][contributors].



[Troubleshooting]()

[commits-shield]: https://img.shields.io/github/commit-activity/y/marrobHD/proxmox-tools.svg?style=for-the-badge
[commits]: https://github.com/marrobHD/proxmox-tools/commits/master
[discord]: https://discord.gg/ND4emRS
[discord-shield]: https://img.shields.io/discord/579704220970909717.svg?style=for-the-badge
[contributors]: https://github.com/marrobHD/proxmox-tools/graphs/contributors
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg?style=for-the-badge
[license-shield]: https://img.shields.io/github/license/marrobHD/proxmox-tools.svg?style=for-the-badge
[maintenance-shield]: https://img.shields.io/badge/maintainer-Marlon-blue.svg?style=for-the-badge
[TechHome]: https://github.com/marrobHD
[releases-shield]: https://img.shields.io/github/release/marrobHD/proxmox-tools.svg?style=for-the-badge
[releases]: https://github.com/marrobHD/proxmox-tools/releases
[esphome]: https://esphome.io
[contributors]: https://github.com/hassio-addons/addon-ssh/graphs/contributors
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg?style=for-the-badge
[license-shield]: https://img.shields.io/github/license/marrobHD/proxmox-tools.svg?style=for-the-badge
[maintenance-shield]: https://img.shields.io/badge/maintainer-Marlon-blue.svg?style=for-the-badge
[releases-shield]: https://img.shields.io/github/release/marrobHD/proxmox-tools.svg?style=for-the-badge
[releases]: https://github.com/marrobHD/proxmox-tools/releases
[twitter]: https://img.shields.io/twitter/follow/TechxHome.svg?style=social
[github]: https://img.shields.io/github/followers/marrobHD.svg?style=social