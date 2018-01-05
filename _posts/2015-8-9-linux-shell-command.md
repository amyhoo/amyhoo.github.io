---
categories: os
tags: [linux]    
---
# authority

# search
## find a command's location
```sh
which 'cmd'
```

# hardware
```bash
# list hardware
lshw
dmidecode –q
# list cpu
lscpu
cat /proc/cpuinfo
# check memory
dmidecode -t memory
# check disk
lsblk
fdisk -l
# check net adapter
lspci | grep -i 'eth'
ethtool eth0
# check bios
dmidecode -t bios
```

# check os
```sh
# check memory
free -m
# check network
ifconfig -a
```