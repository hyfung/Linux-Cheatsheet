# Raspberry Pi Cheatsheet

## Hard-coding Static IP
Location of the configuration file:
> /etc/dhcpcd.conf

```
interface wlan0
static ip_address=192.168.0.4/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1
```

## Hard-coding Hostname
Location of the hostname file:
> /etc/hostname

```
10-x-x-x
```

## Hard-coding Wifi SSID
Location of the configuration file:

> /etc/wpa_supplicant/wpa_supplicant.conf

To edit this file, type
> sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

The content of that file determines which SSID it will connect to automatically.

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=HK

network={
    ssid="SSID_NAME"
    psk="SSID_PASSWORD"
    scan_ssid=1
    key_mgmt=WPA-PSK
}
```

## Enabling SSH in Filesystem Level
`sudo ln -s /lib/systemd/system/ssh.service ssh.service`

## Enable Console Login
```
sudo nano /boot/config.txt

```

Append `enable_uart=1` at the end

## Disabling Screensaver
```bash
sudo nano /etc/lightdm/lightdm.conf
xserver-command=X -s 0 -p 0 -dpms
````

## Enabling GUI in CLI
```bash
sudo apt-get install -y xinit
sudo apt-get install -y lxde-core lxappearance
sudo apt-get install -y lightdm

sudo apt-get install -y pi-greeter raspberrypi-ui-mods raspberrypi-artwork raspberrypi-bootloader
sudo apt-get install -y pix-icons pix-plym-splash pixel-wallpaper
sudo apt-get install -y rpi-chromium-mods
sudo apt-get install -y python-sense-emu python3-sense-emu
sudo apt-get install -y python-sense-emu-doc realvnc-vnc-viewer
sudo reboot
```
