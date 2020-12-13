# PI-RASPBIAN-DOCKSTARTER-CYBERGHOST
Home Media Server on Raspberry Pi, Raspbian Server, Dockstarter and Cyberghost VPN

## AUTOMOUNT A DRIVE
1. **Check Drive**
`sudo fdisk -l`
2. **Check UUID**
`sudo blkid`
3. **Create a mount point**
`sudo mkdir /mnt/hdd`
4. **Edit FSTAB**
`sudo nano /etc/fstab`
5. **Add line**
`UUID=XXXXXXXXXXX  /mnt/hdd    auto nosuid,nodev,nofail,x-gvfs-show 0 0`
6. **Save**
`Ctrl^O + Ctrl^X`
7. **Mount**
`sudo mount -a`

## INSTALL DOCKSTARTER
1. **Update Sources**
`sudo apt-get update`
2. **Upgrade Distro**
`sudo apt-get dist-upgrade`
3. **Install CURL & GIT**
`sudo apt-get install curl git`
4.**Install Docker**
`bash -c "$(curl -fsSL https://get.docker.com)"`
5. **Install DockSTARTer**
`bash -c "$(curl -fsSL https://get.dockstarter.com)"`
6. **Reboot**
^sudo reboot`
