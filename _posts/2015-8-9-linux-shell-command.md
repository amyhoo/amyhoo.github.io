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

## examples
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

# files
lsof -c command
```


## top
 
| pid  | user | priority | nice | virtual mem | reserved mem | shared mem | s | %cpu | %mem | total time | command |
| :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- |
| PID | USER | PR | NI | VIRT  | RES  | SHR  | S |  %CPU |%MEM |  TIME+   | COMMAND      | 
|  1  | root | 20 |  0 |  38104| 6300 |  4124| S |  0.0  | 0.0 |  1:30.51 | systemd      |                                                                                                                   
|  2  | root | 20 |  0 |      0|  0   |   0  | S |  0.0  | 0.0 |  0:00.44 | kthreadd     |                                                                                                                  
|  3  | root | 20 |  0 |      0|  0   |   0  | S |  0.0  | 0.0 |  0:14.70 | ksoftirqd/0  |                                                                                                               
|  5  | root |  0 |-20 |      0|  0   |   0  | S |  0.0  | 0.0 |  0:00.00 | kworker/0:0H |        

## vmstat

| 队列/ 阻塞 | 虚存/空闲/缓存/文件缓存 | 虚存读/虚存写 | 块读/块写 | 中断ps 切换ps | 用户占比/系统占比/空闲/等cpu |
|-|-|-|-|-|-|
| procs | memory | swap | io | system | cpu |
| - | - | - | - | - | - |
|r  b | swpd free   buff  cache | si   so |   bi    bo  | in   cs | us sy id wa st |        
| 0  0 |   832 222808  139776 583184 |   0    0  |   0     5  |  34   26  | 0  0 100  0  0 |
                                                                                              
