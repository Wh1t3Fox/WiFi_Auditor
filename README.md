# WiFi_Auditor
Documenting My Setup for Auditing Wifi Networks, and other Fun Wireless Devices

:construction: Work in Progress  :construction: 

## Hardware
- [Pelican 1400 Case](https://amzn.com/B00009XVKY)
- [RPI 4B 8Gb](https://amzn.com/B08956GVXN)
  - [Argon0ne V2 Case](https://amzn.com/B07WP8WC3V) w/ [SSD Expansion](https://amzn.com/B08MHYWJCP)
  - [WD 500GB Blue M2 SSD](https://amzn.com/B073SBX6TY)
  - [256Gb SanDisk Ultra Micro SD](https://amzn.com/B08GY8NHF2)
- [Panda Wireless PAU09 N600 x2](https://amzn.com/B01LY35HGO)
- [Ubertooth One](https://amzn.com/B07HNMBBST)
- [RTL2832U DVB-T DAB FM & R820T Tuner](https://amzn.com/B00PDM76ZW)
- [GlobalSat BU-353-S4 USB GPS Receiver](https://amzn.com/B008200LHW)
- [Bingfu RP-SMA Male to RP-SMA Female x4](https://amzn.com/B07Z33NJGL)
- [SaiTech IT 2 Pack Short Length 1 Feet USB 3.0 Extension Cable](https://amzn.com/B077MFLH7W)
- [CableCreation 0.5ft 6 inch USB C to A Cable Braided](https://amzn.com/B01CZVEUIE)
- [Unitek 4-Port USB 3.0 Hub](https://amzn.com/B07G9CXSW1)
- [Anker PowerCore 26800 Portable Charger](https://amzn.com/B01JIWQPMW)

<img src="https://raw.githubusercontent.com/Wh1t3Fox/WiFi_Auditor/main/imgs/setup.jpg" width="500" />

## Setup

### 1. OS Installation 
Check out [this](https://gist.github.com/XSystem252/d274cd0af836a72ff42d590d59647928) write-up by XSystem

### 2. Software
#### Dependencies
```bash
sudo pacman -S --noconfirm base-devel git go libpcap libnetfilter_queue libusb gpsd 
```

[yay](https://github.com/Jguer/yay)
```bash
git clone https://aur.archlinux.org/yay.git
cd yay && makepkg -si
```

[archstrike](https://archstrike.org/)
```bash
sudo su -
echo -e '[archstrike]\nServer = https://mirror.archstrike.org/$arch/$repo' >> /etc/pacman.conf
pacman -Syy
pacman-key --init
dirmngr < /dev/null
pacman-key -r 9D5F1C051D146843CDA4858BDE64825E7CBC0D51
pacman-key --lsign-key 9D5F1C051D146843CDA4858BDE64825E7CBC0D51
pacman -S archstrike-keyring
pacman -S archstrike-mirrorlist
sed -i 's|Server = https://mirror.archstrike.org/$arch/$repo|Include = /etc/pacman.d/archstrike-mirrorlist|' /etc/pacman.conf
pacman -Syy
```

#### Wifi Tools
[bettercap](https://bettercap.org)
```bash
go get github.com/bettercap/bettercap
cd $GOPATH/src/github.com/bettercap/bettercap
make build
sudo make install
sudo bettercap -eval 'caplets.update; ui.update; q'
sudo cp ./caplets/* /usr/local/share/bettercap/caplets
sudo cp ./bin/bettercap-launcher /usr/local/bin/
sudo cp ./systemd/bettercap@.service /etc/systemd/system/
sudo systemctl daemon-reload
```

#### Bluetooth Tools


#### SDR Tools

