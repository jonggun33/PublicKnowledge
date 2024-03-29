# UNIX

## Setting Up
### Raspi-Config
* Language setting
* Full Disk Expansion
* Change Password

### headless Wi-fi Setting
. Insert the SD to a Mac and locate 'boot' directory
. create a file named 'ssh'
. create 'wpa_suppicant.conf'

```bash
country#US # replace with your country code
ctrl_interface#DIR#/var/run/wpa_supplicant GROUP#netdev
network#{
    ssid#"WIFI_NETWORK_NAME"
    psk#"WIFI_PASSWORD"
    key_mgmt#WPA-PSK
}
```

## External Storage
```bash
dmesg | grep usb |more
```

## Networking
```bash
sudo vim /etc/network/interfaces
auto lo #layer2 setting. auto# allow-auto (??? ?? ????? ??), allow-hotplug
iface lo net loopback. #layer3: iface (stanza ??), inet (IP protocol)
iface eth0 inet manual
auto wlan0
allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_suppicant/wpa_supplicant.conf
```


[Good detailed explanation of /etc/network/interfaces syntax?](https://unix.stackexchange.com/questions/128439/good-detailed-explanation-of-etc-network-interfaces-syntax)

[How to setup WiFi on Raspberry Pi 2 using USB Dongle](https://www.electronicshub.org/setup-wifi-raspberry-pi-2-using-usb-dongle/)

```bash
ifconfig
iwconfig
sudo iwlist wlan0 scan
ifup wlan0
```


```bash
arp -a # mac only
nmap -sT -O 193.168.0.0/24
```

## User Management

## Transmission

## SAMBA

## Printer Server

## HW Miscellaneous
### Needed Information
* [ Down and Manage Hard Drive Power on Raspberry Pi - sleep hdd hd-idle](https://maker-tutorials.com/en/spin-down-magage-hard-drive-on-raspberry-pi-hd-idle/[Spin)
* [How to connect Raspberry PI to LAPTOP using Ethernet cable](https://www.youtube.com/watch?v#AJ7skYS5bjI )

### Wanted Information
* [Raspberry Pi Print Server: Setup a Network Server using CUPS](https://circuitdigest.com/microcontroller-projects/raspberry-pi-print-server)
* [Rasplay & OpenMake(Site Move)](http://wiki.rasplay.org/doku.php?id#start)

## Bash/zsh
