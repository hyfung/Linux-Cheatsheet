# ip Command Cheatsheet

## IP queries
`ip addr`  
`ip addr show dev INT`  
Show information for addresses

`ip link`  
`ip link show dev INT`  
`ip -s link`  
Show state of interfaces

`ip route`  
Show routing table

`ip maddr`  
`ip maddr show dev INT`  
Show multicast information

`ip neight`  
`ip neigh show dev INT`  
Show neighbourship (ARP Table)

`ip help`  
Show a list of command

## Multicast addressing
`ip maddr {add|del} {MAC_ADDR} dev INT`  
Add or delete a multicast address

## Modifying address and link properties
`ip addr {add|del} {IP/MASK} dev INT`  

`ip link set INT up|down`  
`ip link set INT mtu 9000`  
`ip link set INT promisc on|off`  

## Adjusting and viewing routes

`ip route add default via IP dev INT`  
`ip route add|delete IP/MASK via IP`  
`ip route add|delete IP/MASK dev INT`  
`ip route replace IP/MASK dev INT`  
`ip route get DEST`  

## Managing ARP table

`ip neigh add IP lladdr MAC dev INT`  
`ip neigh del IP dev INT`  
`ip neigh replace IP lladdr MAC dev INT`  

## Useful network commands

### arping (Send ARP request to neighbour hosts)
`arping -I eth0 192.168.0.1`  
Send ARP request to IP via Interface

`arping -D -I eth0 192.168.0.1`  
Check for duplicate MAC at IP on Interface

### ethtool (Query/control network drivers and hardware)
`ethtool -g eth0`  
Display ring buffer for eth0

`ethtool -i eth0`  
Display driver information for eth0

`ethtool -p eth0`  
Identify eth0 by blinking LED

`ethtool -S eth0`  
Display network and driver statistics


### ss (Socket statistics)
`ss -a`  
Show all sockets

`ss -e`  
Show detailed socket information

`ss -o`  
Show timer information

`ss -n`  
Do not resolve address

`ss -p`  
Show process using the socket

## net-tools VS iproute
|Net-tools                                                  |iproute                                                |
|-----------------------------------------------------------|-------------------------------------------------------|
|arp -a                                                     |ip neigh                                               |
|arp -v                                                     |ip -s neigh                                            |
|arp -s 192.168.0.1 1:2:3:4:5:6                             |ip neight add 192.168.0.1 lladdr 1:2:3:4:5:6 dev eth1  |
|arp -i eth1 -d 192.168.0.1                                 |ip neigh del 192.168.0.1 dev eth1                      |
|ifconfig -a                                                |ip addr                                                |
|ifconfig eth0 down                                         |ip link set eth0 down                                  |
|ifconfig eth0 up                                           |ip link set eth0 up                                    |
|ifconfig eth0 192.168.0.1                                  |ip addr add 192.168.0.1/24 dev eth0                    |
|ifconfig eth0 netmask 255.255.255.0                        |ip addr add 192.168.0.1/24 dev eth0                    |
|ifconfig eth0 mtu 9000                                     |ip link set eth mtu 9000                               |
|ifconfig eth0:0 192.168.1.2                                |ip addr add 192.168.1.2/24 dev eth0                    |
|netstat                                                    |ss                                                     |
|netstat -neopa                                             |ss -neopa                                              |
|netstat -g                                                 |ip maddr                                               |
|route                                                      |ip route                                               |
|route add -net 192.168.1.0 netmask 255.255.255.0 dev eth0  |ip route add 192.168.1.0/24 dev eth0                   |
|route add default gw 192.168.1.1                           |ip route add default via 192.168.1.1                   |

# Setting static IP in Ubuntu

## Using ifconfig:
```
ifconfig eth0 192.168.0.100 netmask 255.255.255.0 up
route add default gw 192.168.1.1
echo "nameserver 1.1.1.1" > /etc/resolv.conf
```

## Using ip and netplan
> `/etc/cloud/cloud.cfg.d/subiquity-disable-cloudinit-networking.cfg`
```
network: {config: disabled}
```

```
ip addr show
ip link set eth0 up
ip link set eth1 down
ip route show
```

> `/etc/netplan/00-installer-config.yaml`
```
network:
  ethernets:
      eno1:
          addresses: [192.168.1.13/24]
          gateway4: 192.168.1.1
          dhcp4: true
          optional: true
          nameservers:
              addresses: [8.8.8.8,8.8.4.4]
  version: 2
```

> netplan apply

# Setting static IP in Raspberry Pi

## Modify /etc/wpa_supplicant/wpa_supplicant.conf
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=HK

network={
    ssid="SSID_NAME"
    psk="SSID_PASSWORD"
    key_mgmt=WPA-PSK
    scan_ssid=1
}
```

## Modify /etc/dhcpcd.conf
```
interface wlan0
static ip_address=192.168.0.4/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1
```

## Modify /etc/hostname
```
HOSTNAME
```
