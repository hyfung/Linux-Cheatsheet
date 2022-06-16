# iptable Cheatsheet for Ubuntu

## Blocking ports
```bash
iptables -A INPUT -p tcp --destination-port 6379 -j DROP
iptables -D INPUT {index}
```

##

##


## Rejection Type
```
--reject-with TYPE
    icmp-net-unreachable
    icmp-host-unreachable
    icmp-port-unreachable
    icmp-proto-unreachable
    icmp-net-prohibited
    icmp-host-prohibited or
    icmp-admin-prohibited (*)
```
