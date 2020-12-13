# PI-RASPBIAN-DOCKSTARTER-CYBERGHOST
Home Media Server on Raspberry Pi, Raspbian Server, Dockstarter and Cyberghost VPN

## AUTOMOUNT AN EXTERNAL USB DRIVE
1. **Locate Partition**
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
`sudo reboot`

## INSTALL OPENVPN
1. **Update & Upgrade**
`sudo apt-get update && sudo apt-get upgrade`
2. **Install Dependencies**
`sudo apt-get install openvpn openssl openresolv`
3. **Create a credentials file**
`sudo nano user.txt`
4. **Add credentials to user.txt**
```
USER
PASSWORD
```
5. **Copy config files to /etc/openvpn**
```
sudo cp CG_XX.conf /etc/openvpn/
sudo cp ca.crt /etc/openvpn/
sudo cp client.crt /etc/openvpn/
sudo cp client.key /etc/openvpn/
sudo cp user.txt /etc/openvpn/
```
6. **Add VPN tun driver**
```
echo "iptable_mangle" | sudo tee /etc/modules-load.d/iptable_mangle.conf
echo "tun" | sudo tee /etc/modules-load.d/tun.conf
```
7. **Reboot***
`sudo reboot`
