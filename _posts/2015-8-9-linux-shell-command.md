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
## list software  
```sh
#
dpkg -l
dpkg --list
dpkg --get-selections
# server
service --status-all
initctl list
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

# str operation
```sh
# string conclude   
[[ "abcabc" =~ "abc" ]] && echo yes
# find line
grep regex filename
# split,get columne
echo a,b,c | cut -d, -f2
echo a,b,c | awk -F"," '{print $2}' 
```

# performance monitor
![monitor_tools_linux](/assets/img/monitor_tools_linux.jpg)

```sh
# cpu: User Time <= 70%，System Time <= 35%，User Time + System Time <= 70%
# cpu: 3 or less thread  each cpu
# memory: swap in == 0 swap out == 0  free /total <=70%	
# disk iowait % < 20% ,packages lost
# network not so much waiting 
vmstat 
free

# udp lost packages
watch netstat -su
watch netstat -lunp
#  tcp RetransSegs / OutSegs
cat /proc/net/snmp | grep Tcp:

```