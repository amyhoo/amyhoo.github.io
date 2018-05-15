---
categories: os
tags: [linux]    
---

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

| 进程队列 /阻塞队列 | 虚存/空闲/缓存/文件缓存 | 虚存读/虚存写 | 块读/块写 | 中断ps 切换ps | 用户占比/系统占比/空闲/等cpu |
|-----|-----|--------|---------|----------|-------------|------------|
| proc| memory | swap | io | system | cpu |
| - | - | - | - | - | - |
|r,b | swpd,free,buff,cache | si,so |   bi,bo  | in,cs | us,sy,id,wa,st |        
| 0,0 | 832,222808,139776,583184 | 0,0 | 0,5 | 34,26 | 0,0，100,0,0 |

## lsof
```sh
lsof -c bash | awk '{print $1"|"$2"|"$3"|"$4"|"$5"|"$6"|"$7"|"$8"|<sub>"$9"</sub>|"}'
```

COMMAND|PID|USER|FD|TYPE|DEVICE|SIZE/OFF|NODE|NAME|
-|-|-|-|-|-|-|-|-|
bash|31785|root|cwd|DIR|253,1|4096|775|<sub>/root</sub>|
bash|31785|root|rtd|DIR|253,1|4096|2|<sub>/</sub>|
bash|31785|root|txt|REG|253,1|1037528|129541|<sub>/bin/bash</sub>|
