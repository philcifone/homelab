# Proxmox VE - .179:8006

## Storage

#### local

#### local-lvm
- Thin provisioned:

#### magellan - (4) 1TB disks
- RAIDz1 - 3TB

#### catalyst - (4) 6TB disks
- RAIDz1 - 18TB

#### smb-catalyst 
- 7500TB (CT 104 filebrowser)
#### smb-magellan 
- 512GB (CT 104 filebrowser)

### Backups

- snapshots of all containers at 0300; 1530 to smb-magellan
- snapshots of all containers at 1500 to local

### Cronjob

- rsync local container backup push to /gamehenge/computer


### Debian/Ubuntu Container Startup:

```shell
adduser phil
```
```shell
passwd phil
```
usermod -aG sudo phil

su - phil

sudo apt update && sudo apt dist-upgrade -y

sudo apt install vim sudo git rsync htop
```

### Arch Container Startup:

```shell
pacman-key --init

pacman-key --populate

pacman-key --refresh-keys

pacman -Syu vim sudo git rsync htop neofetch

useradd -m -g users -G wheel phil

passwd phil

EDITOR=vim visudo <uncomment sudo for wheel users>

su - phil
```

## Container List

### 100 photoprism - photo database - .189:2342
- Distro: Debian
- Storage: /mnt/catalyst - 1TB = direct
- notes:
  cronjob rsync catalyst pull from gamehenge analog
  magical config file: /var/lib/photoprism/.env

### 101 wireguard - personal VPN
- Distro: Ubuntu


### 103 plex - media server - .128:32400 
- Distro: Ubuntu
- Storage: /mnt/catalyst - 5TB = direct
- notes:
	- cronjob rsync catalyst push to gamehenge ISOs
	- cronjob rsync catalyst pull from gamehenge movies
	- cronjob rsync catalyst pull from gamehenge shows

### 104 filebrowser & samba file share - .164:8080
- Distro: Debian
- Storage0: /mnt/catalyst - 5TB = direct > smb
- Contents0: Mirror of (most of) /Volumes/Gamhenge from .187
- Storage1: /mnt/magellan - 512GB = direct > smb
- Contents1: Snapshot images of containers


### 106 philcifone.com - web server - .144:1313
- Distro: Arch
- Web server: Nginx
- Framework: Hugo


### 108 - web server
(offline / in development)

### 109 - web server (offline)
(offline / in development)

#### references & links:
learnlinuxTV
homelab.show
networkchuck
unix & linux system administration handbook
all Linux no starch press publications

ZFS DRIVE REPLACEMENT IF NEEDED
https://docs.tritondatacenter.com/private-cloud/troubleshooting/disk-replacement
