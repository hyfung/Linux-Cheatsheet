# Useful Commands in Ubuntu

## Process Management

#### htop
|Hotkey |Function|
|-|-|
|E|Show ENV variables|
|U|Select User|
|I|IO Priority|



## User Management
Create a new user
```bash
# Adding new user
sudo useradd jerry --home-dir /home/jerry

sudo useradd dummy --shell=/sbin/nologin

# Use adduser instead to auto create directory and setting password

# Changing password
sudo passwd jerry

```

```
sudo usermod -s SHELL_NAME
```

## Capturing Input
Opens a widget and displays input event in terminal
`xev`

## Mounting Volumes
CIFS/Samba
> `sudo mount -t cifs -o username=${USERNAME},password=${PASSWORD},uid=${UID},gid=${GID} ${REMOTE_PATH} ${MNT_PT}`

SSHFS
> `ssh://root@HOST:PORT/MOUNTPOINT`

> `sshfs root@192.168.0.210:/mnt/Vault Vault -p 4096`

## User and Group

```bash
id //Reveals everything
id -u USERNAME //Get user id
id -g USERNAME //Get primary group id
id -G USERNAME //Get all groups
id -Gn //Show all groups of this PC
```

## GRUB
Edit `/etc/default/grub`
```
update-grub
update-initramfs
```

## Rsync
```bash
rsync -r SRC DST //Doing it locally
rsync [USER@HOST:SRC] DST
rsync SRC [USER@HOST:DST]
--delete //Remove non-existent files
--ignore-existing //Skip updating new files
--existing //Skip creating new files
--progress
```

## Manually Installing SSH Service
```
Created symlink /etc/systemd/system/sshd.service → /lib/systemd/system/ssh.service
Created symlink /etc/systemd/system/multi-user.target.wants/ssh.service → /lib/systemd/system/ssh.service
```

## Process Management

Show all running processes
```bash
ps -ef
ps aux
```

Get PID by process name
```
pgrep
```

## Useful Commands In Terminal
List all audio devices
> `aplay -l`

Getting unique lines only
> ` |uniq`

Sorting lines
> `| sort`

Pretty-print a JSON
> `python3 -m json.tool ${JSON_FILE}`

> `cat ${JSON_FILE} | python3 -m json.tool`

Get value from white-spaced columns
> `cut -d ' ' -f ${INDEX}`

Replacing string
> `| sed 's/${SRC}/${DST}/g'`

Grep only matched part
> `| grep -o ${PATTERN}`

Decoding B64
> `cat ${FILE} | base64 -d`

Creating filesystems
```bash
mkfs.exfat -F -O ^64bit -L ${LABEL} '...' /dev/sdX
mkfs.exfat -n NAME -s SECTOR /dev/sdX
```

Netcat
```bash
nc -lkv ${PORT}

-l Listen
-k Keep
-v Verbose
```

Date
```bash
date +%Y-%m-%d
```

## Recording RTSP via FFMPEG
```bash
while true;
do
    ffmpeg -i rtsp://cfb095:tplink123123@192.168.1.10/stream1 \
    -t 3600 -r 10 $(date +%Y%m%d-%H%M%S).mp4
done
```

## Setting and Getting Date In CLI
```bash
date +%Y%m%d-%H%M%S
```

```bash
date -s "2020-01-01 00:00:00"
```

## Creating & Restoring HDD Images

### Basic Form Using DD
`sudo dd if=/dev/sda of=sda.img status=progress oflag=nocache`
`sudo dd if=sda.img of=/dev/sda status=progress`

### Creating
`sudo dd if=/dev/sda bs=4M oflag=nocache status=progress | gzip -c | split -B 4095M NAME.tar.gz.`

### Restoring
`sudo dd if=/dev/sda bs=4M oflag=nocache status=progress | gzip -c | split -B 4095M NAME.tar.gz.`

## IP Related (Layer 3)

Extracting MAC Address of an interface
> `ifconfig ${INTERFACE_NAME}| grep ether | grep -o '[0-9a-f]\+\:[0-9a-f]\+\:[0-9a-f]\+\:[0-9a-f]\+\:[0-9a-f]\+\:[0-9a-f]\+' | sed -r 's/://g'`

> `cat /sys/class/net/${INTERFACE_NAME}/address | sed -r 's/://g'`

Extracting IP Address of an interface
> `ifconfig ${INTERFACE_NAME}| grep -o 'inet \w*\.\w*\.\w*\.\w*' | grep -o '\w*\.\w*\.\w*\.\w*'`

> `ifconfig ${INTERFACE_NAME}| grep -o 'inet \w*\.\w*\.\w*\.\w*' | grep -o '\(\w*\.\)\{3\}\w*'`

> `ip addr show dev ${INTERFACE_NAME} | grep -o 'inet \w*\.\w*\.\w*\.\w*' | grep -o '\w*\.\w*\.\w*\.\w*'`

## Get MAC Addresses From /sys/class (Layer 2)

|Name   |Destination            |
|-------|-----------------------|
|       |/sys/class/phy         |
|       |/sys/class/ieee80211   |
|       |/sys/class/backlight   |

## Useful Commands In GCC

Generating assembly code
> `gcc ... -S -fverbose-asm`

Generate object code
> `gcc -c FILE.c -o FILE.o`

Generating linker map
> `gcc ... -Xlinker -Map=output.map`

Inspecting an object file
> `objdump -x an_object_file.o`

Disassemble an object file
> `objdump -D an_object_file.o`

Reading ELF header
> `readelf -h FILENAME.o`

Reading Session header
> `readelf -S FILENAME.o`

Readung Program Header
> `readelf -l EXECUTABLE`

## Service & Systemd

Show all services  
> `systemctl`

Show systemd journal
> `journalctl -xe`

Manually enabling a service  
Adding a symlink from /etc/systemd/system to  
> `/etc/systemd/system/multi-user.target.wants`

Systemd Service Template
```bash
[Unit]
Description=Example Service
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
Environment=DISPLAY=:0
WorkingDirectory=/
ExecStart=/bin/bash /tmp/foo.sh #Abs path to command
Restart=Always/Once/No #Does the service restarts
RestartSec=100 #Time to wait before restart
TimeoutSec=100 #
User= #root

[Install]
WantedBy=multi-user.target
```

## Disable/Enable GUI

```bash
sudo systemctl set-default multi-user

sudo systemctl set-default graphical

sudo systemctl start gdm3
```

## Network Manager (nmcli)


## Kernel

Show kernel ring buffer
> `dmesg`

## PythonQt

```bash
sudo apt install Qtcreator
pyuic5 UIFILE.UI -x > PYTHON.PY
```

## PyInstaller
```bash
pyinstaller source.py
pyinstaller --onefile source.py
```

## Virtualbox
VBox mount raw disk
`vboxmanage internalcommands createrawvmdk -filename "</path/to/file>.vmdk" -rawdisk /dev/sda`

Convert VHD/VDI to IMG
`vboxmanage clonehd SRC.vdi --format raw DST.img`

## FFmpeg

Transcoding video with Intel Quick Sync
`ffmpeg -vaapi_device /dev/dri/renderD128 -i $1 -vf 'format=nv12,hwupload' -c:v h264_vaapi $1.mp4`

Transcoding video with H264 nvenc
`ffmpeg -i input.avi -c:v h264_nvenc output.mp4`

## VLC
Play and exit
```bash
export DISPLAY=:0
cvlc --play-and-exit --fullscreen $1
```

```bash
cvlc rtsp://cfb095:tplink123123@192.168.1.10/stream2
```

## Enabling Console Login

Plain-old executable
`agetty /dev/ttyUSB0 115200`

or service

`sudo nano /lib/systemd/system/serial-getty@.service`

```bash
# Edit this line
ExecStart=-/sbin/agetty --keep-baud 115200,38400,9600 %I $TERM

# To This
ExecStart=-/sbin/agetty 115200 %I $TERM
```

```bash
systemctl daemon-reload

# For a USB serial adaptor
systemctl enable serial-getty@ttyUSB0.service

# For a built in serial port /dev/ttyS0
systemctl enable serial-getty@ttyS0.service
```


# Useful Commands in FreeBSD
Disk Management
```bash
geom disk list
kldload fuse //Optional
mount_ntfs VOLUME MOUNTPOINT
mount_ntfs dev/disk/label mountpoint
mount -t ntfs-3g VOL MNT
```

# Arduino

```bash
avrdude -p ${MCU_MODEL} -c ${PROGRAMMER}
avrdude -U ${TYPE}:{R|W}:filename:format

MCU: m32u4, m328p
TYPE: eeprom, flash, fuse, lfuse, hfuse
PROGRAMMER: usbasp
```
