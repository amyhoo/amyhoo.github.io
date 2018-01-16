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
```sh
# list hardware
lshw
lshw -class network
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
# check os version
uname -a
cat /proc/version
```

# check file
```sh
# what the encode 
enca {filename}
# check conf definition,ignore #
grep -v "^#" file_path
```

# process
```sh
# show process tree
ps axjf
pstree

# show resource occupation
ps aux
ps -aux --sort -pcpu |less
ps -aux --sort -pmem |less

# show all
ps -A
ps -e

#
ps -a  
ps
```

# net information
```sh
# show 
netstat -apn | grep :8080
# show listen port
netstat -l | grep :8080
```