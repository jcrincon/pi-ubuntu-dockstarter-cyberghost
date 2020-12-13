# pi-ubuntu-dockstarter-cyberghost
Home Media Server on Raspberry Pi, Ubuntu 18.04 Server, Cyberghost VPN

## AUTOMOUNT A DRIVE
1. Check Drive
`sudo fdisk -l`
2. Check UUID
`sudo blkid`
3. Create a mount point
`sudo mkdir /mnt/hdd`
4. Edit FSTAB
`sudo nano /etc/fstab`
5. Add line:
`UUID=XXXXXXXXXXX  /mnt/hdd    auto nosuid,nodev,nofail,x-gvfs-show 0 0`
6. Save
`Ctrl^O + Ctrl^X`
7. Mount
`sudo mount -a`
