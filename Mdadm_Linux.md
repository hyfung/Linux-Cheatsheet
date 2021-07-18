# Linux Software RAID with mdadm

## General Command Used


## Full Setup Guide

### Creating a RAID
```
mdadm -C /dev/md0 -a yes -l 1 -n 2 /dev/sda /dev/sdb
```

### Editing /etc/fstab to Automount

