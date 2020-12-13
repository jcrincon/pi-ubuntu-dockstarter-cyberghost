# PI-RASPBIAN-DOCKSTARTER-CYBERGHOST
Home Media Server on Raspberry Pi, Raspbian Server, Dockstarter and Cyberghost VPN

## CREATE RASPBIAN IMAGE ON SD CARD
1. 

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
3. **Add VPN tun driver**
```
echo "iptable_mangle" | sudo tee /etc/modules-load.d/iptable_mangle.conf
echo "tun" | sudo tee /etc/modules-load.d/tun.conf
```
4. **Reboot***
`sudo reboot`

## CONFIGURE CYBERGHOST
1. **Create a credentials file**
`sudo nano user.txt`
2. **Add credentials to user.txt**
```
USER
PASSWORD
```
3. **Save & Exit**
`Ctrl^O + Ctrl^X`
4. **Copy config files to /etc/openvpn**
```
sudo cp CG_XX.conf /etc/openvpn/
sudo cp ca.crt /etc/openvpn/
sudo cp client.crt /etc/openvpn/
sudo cp client.key /etc/openvpn/
sudo cp user.txt /etc/openvpn/
```
5. **Edit Configuration**
`sudo nano CG_XX.conf`
6. **Extend the line ‘auth-user-pass’**
From:
```
[...]
auth-user-pass
[...]
```
To:
```
[...]
auth-user-pass /etc/openvpn/user.txt
[...]
```
At the bottom of the configuration passage (after 'verb 4') add the following two lines:
```
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf
```
7. **Save & Exit**
`Ctrl^O + Ctrl^X`
8. **Autoload config**
Open default config
`sudo nano /etc/default/openvpn`
And adding the following line:
`AUTOSTART="CG_XX"`
(the name of the file WITHOUT the file extension ‘.conf’)
9. **Save & Exit**
`Ctrl^O + Ctrl^X`

## STARTUP OPENVPN
1. **Enable OpenVPN**
`sudo update-rc.d openvpn enable`
2. **Start Service**
`sudo service openvpn start`
3. **Check Status of OpenVPN Connection**
`systemctl status openvpn@CG_XX`
4. **Check IP**
`curl ifconfig.me`
5. **Perform a DNS Leak Test**
`curl https://ipleak.net/json/`
