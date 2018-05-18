---
categories: os
tags: [linux]    
---

# system performance monitor
![monitor_tools_linux](/assets/img/monitor_tools_linux.jpg)

## examples
```sh
# cpu: User Time <= 70%，System Time <= 35%，User Time + System Time <= 70%
# cpu: 3 or less thread  each cpu
# memory: swap in == 0 swap out == 0  free /total <=70%	 
vmstat 
free
top
cat /proc/meminfo

# network not so much waiting 
tcpdump -i eth0
# udp lost packages
watch netstat -su
watch netstat -lunp
#  tcp RetransSegs / OutSegs
cat /proc/net/snmp | grep Tcp:
traceroute ip 

# disk iowait % < 20% ,packages lost
iostat
# files
lsof -c command
df
du
fdisk -l
#process
strace -p pid
pmap pid
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

| 进程队列 /阻塞队列 | 虚存/空闲/缓存/文件缓存 | 虚存读/虚存写 | 块读/块写 | 中断ps 切换ps | 用户占比/系统占比/空闲/等cpu |
|-----|-----|--------|---------|----------|-------------|------------|
| proc| memory | swap | io | system | cpu |
| - | - | - | - | - | - |
|r,b | swpd,free,buff,cache | si,so |   bi,bo  | in,cs | us,sy,id,wa,st |        
| 0,0 | 832,222808,139776,583184 | 0,0 | 0,5 | 34,26 | 0,0，100,0,0 |

## lsof
```sh
lsof -c bash | awk '{print "<sub>"$1"</sub>|<sub>"$2"</sub>|<sub>"$3"</sub>|<sub>"$4"</sub>|<sub>"$5"</sub>|<sub>"$6"</sub>|<sub>"$7"</sub>|<sub>"$8"</sub>|<sub>"$9"</sub>"}'
```
COMMAND|PID|USER|FD|TYPE|DEVICE|SIZE/OFF|NODE|NAME|
-|-|-|-|-|-|-|-|-|
bash|31785|root|cwd|DIR|253,1|4096|775|<sub>/root</sub>|
bash|31785|root|rtd|DIR|253,1|4096|2|<sub>/</sub>|
bash|31785|root|txt|REG|253,1|1037528|129541|<sub>/bin/bash</sub>|

## netstat 
```sh
# all
netstat -a 
netstat -ano
netstat -at
netstat -au
# show process
netstat -p
# statics
netstat -s
# listen
netstat -l
```

|Proto|Recv-Q|Send-Q|Local Address|Foreign Address|State|
|-|-|-|-|-|-|-|-|
|tcp|0|0|localhost:9000|*:*|LISTEN|-|<sub>off</sub>|
|tcp|0|0|localhost:6379|*:*|LISTEN|-|<sub>off</sub>|
|tcp|0|0|*:18000|*:*|LISTEN|-|<sub>off</sub>|
|tcp|0|0|*:18001|*:*|LISTEN|-|<sub>off</sub>|
|tcp|0|0|*:ssh|*:*|LISTEN|-|<sub>off</sub>|

## iostat

|avg-cpu:|%user|%nice|%system|%iowait|%steal|%idle|
|-|-|-|-|-|-|-|
||5.73|0.00|2.84|0.03|0.00|91.40|

|Device:|tps|kB_read/s|kB_wrtn/s|kB_read|kB_wrtn|
|-|-|-|-|-|-|
|sda|3.04|6.34|35.04|38246980|211280790|
|scd0|0.13|2.28|0.00|13755852|0|
|dm-0|0.02|0.54|1.43|3247725|8593033|

## free

| |       total  |      used   |     free   |   shared | buff/cache  | available
|Mem:|        8157556|      586440|     4970848|       33752|     2600268|     7176188
|Swap:|      7811068 |          0 |    7811068 |

# process monitor
```sh
ps -p pid -o %cpu,%mem,cmd
ps -C chrome -o %cpu,%mem,cmd
```