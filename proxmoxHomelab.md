# Proxmox VE - .179:8006

## Storage

**local**

**local-lvm**
- Thin provisioned:

**magellan** - (4) 1TB disks
- RAIDz1 - 3TB

**catalyst** - (4) 6TB disks
- RAIDz1 - 18TB

**smb-catalyst** 
- 7500TB (CT 104 filebrowser)

**smb-magellan** 
- 512GB (CT 104 filebrowser)

## Backups

- up to 15 daily,weekly, monthly, and yearly snapshots of all containers at 0300; 1530 to smb-magellan
- snapshots of all containers at 1500 to local

**cronjobs**

- rsync backup push from local to 10.0.0.187/gamehenge/computer

## Firewalls

- icmp (ping) 10.0.0.xx/32
- tcp (web interface) global :8006
- ssh (secure shell) 10.0.0.xx/32, 10.0.0.xxx/32
<br>

## Debian/Ubuntu Container Startup:

add user phil
```shell
adduser phil
```
<br>

set password for phil
```shell
passwd phil
```
<br>

add phil to sudo group
```shell
usermod -aG sudo phil
```
<br>

login to phil
```shell
su - phil
```
<br>

system update && upgrade
```shell
sudo apt update && sudo apt dist-upgrade -y
```
<br>

install packages
```shell
sudo apt install vim sudo git rsync htop neofetch
```
<br>

## Arch Container Startup:

initalize package keyring
```shell
pacman-key --init
```
<br>

populate keyring
```shell
pacman-key --populate
```
<br>

refresh keyring
```shell
pacman-key --refresh-keys
```
<br>

update system and install packages
```shell
pacman -Syu vim sudo git rsync htop neofetch base-devel
```
<br>

add user phil
```shell
useradd -m -g users -G wheel phil
```
<br>

set password for phil
```shell
passwd phil
```
<br>

uncomment wheel entry for sudo privledges
```shell
EDITOR=vim visudo 
```
<br>

login to phil
```shell
su - phil
```
<br>

## Container List

### 100 photoprism - photo database - .189:2342
- Distro: Debian
- Storage: /mnt/catalyst - 1TB = direct
- Firewall: ssh 10.0.0.xx/32, 10.0.0.xx/32
- notes:
	- built with a tteck script
	- cronjob rsync catalyst pull from gamehenge analog
	- magical config file: /var/lib/photoprism/.env

### 101 wireguard - personal VPN
- Distro: Ubuntu
- Firewall: ssh 10.0.0.xx/32, 10.0.0.xxx/32


### 103 plex - media server - .128:32400 
- Distro: Ubuntu
- Storage: /mnt/catalyst - 5TB = direct
- Firewall: ssh 10.0.0.xx/32, 10.0.0.xxx/32
- cronjob:
	- rsync catalyst push to gamehenge ISOs
	- rsync catalyst pull from gamehenge movies
	- rsync catalyst pull from gamehenge shows

### 104 filebrowser & samba file share - .164:8080
- Distro: Debian
- Storage0: /mnt/catalyst - 5TB = direct > smb
- Contents0: Mirror of (most of) /Volumes/Gamhenge from .187
- Storage1: /mnt/magellan - 512GB = direct > smb
- Contents1: Snapshot images of containers
- Firewall: ssh 10.0.0.xx/32, 10.0.0.xxx/32


### 106 [philcifone.com](https://philcifone.com) - web server - .144:1313
- Distro: Arch
- Web server: Nginx
- Framework: Hugo
- Firewall: 
	- ssh 10.0.0.xx/32, 10.0.0.xxx/32
	- https global

#### Hugo commands:

test server changes before pushing live
```shell
hugo server --baseURL 10.0.0.144 --bind 10.0.0.144
```
<br>

new blog, automatically created inside "content" directory
```shell
hugo new blog/<title.md>
```
<br>

open blog to edit in vim
```shell
sudo vim content/blog/<title.md>
```
<br>

push live
```shell
sudo hugo
```

### 108 - web server
(offline / in development)

### 109 - web server (offline)
(offline / in development)
<br>

#### references & links:
- learnlinuxTV - Jay Lacroix
- lawrence systems - Tom Lawrence
- homelab.show
- networkchuck
- unix & linux system administration handbook
- pretty much every Linux no starch press publication

##### ZFS drive replacement
- https://docs.tritondatacenter.com/private-cloud/troubleshooting/disk-replacement
