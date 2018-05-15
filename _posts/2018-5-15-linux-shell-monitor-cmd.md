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
lsof -c bash | awk '{print $1"|"$2"|"$3"|"$4"|"$5"|"$6"|"$7"|"$8"|"$9"|"}'
```

COMMAND|PID|USER|FD|TYPE|DEVICE|SIZE/OFF|NODE|NAME|
-|-|-|-|-|-|-|-|-|
bash|24738|test|cwd|DIR|8,2|4096|526971|/home/test|
bash|24738|test|rtd|DIR|8,2|4096|2|/|
bash|24738|test|txt|REG|8,2|1037528|131074|/bin/bash|
bash|24738|test|mem|REG|8,2|47600|4990794|/lib/x86_64-linux-gnu/libnss_files-2.23.so|
bash|24738|test|mem|REG|8,2|47648|4990797|/lib/x86_64-linux-gnu/libnss_nis-2.23.so|
bash|24738|test|mem|REG|8,2|93128|4990790|/lib/x86_64-linux-gnu/libnsl-2.23.so|
bash|24738|test|mem|REG|8,2|35688|4990803|/lib/x86_64-linux-gnu/libnss_compat-2.23.so|
bash|24738|test|mem|REG|8,2|2981280|4854619|/usr/lib/locale/locale-archive|
bash|24738|test|mem|REG|8,2|1868984|4990813|/lib/x86_64-linux-gnu/libc-2.23.so|
bash|24738|test|mem|REG|8,2|14608|4990802|/lib/x86_64-linux-gnu/libdl-2.23.so|
bash|24738|test|mem|REG|8,2|167240|4981342|/lib/x86_64-linux-gnu/libtinfo.so.5.9|
bash|24738|test|mem|REG|8,2|162632|4990791|/lib/x86_64-linux-gnu/ld-2.23.so|
bash|24738|test|mem|REG|8,2|26258|4858348|/usr/lib/x86_64-linux-gnu/gconv/gconv-modules.cache|
bash|24738|test|0u|CHR|136,0|0t0|3|/dev/pts/0|
bash|24738|test|1u|CHR|136,0|0t0|3|/dev/pts/0|
bash|24738|test|2u|CHR|136,0|0t0|3|/dev/pts/0|
bash|24738|test|255u|CHR|136,0|0t0|3|/dev/pts/0|
bash|24805|root|cwd|DIR|8,2|4096|2883585|/root|
bash|24805|root|rtd|DIR|8,2|4096|2|/|
bash|24805|root|txt|REG|8,2|1037528|131074|/bin/bash|
bash|24805|root|mem|REG|8,2|47600|4990794|/lib/x86_64-linux-gnu/libnss_files-2.23.so|
bash|24805|root|mem|REG|8,2|47648|4990797|/lib/x86_64-linux-gnu/libnss_nis-2.23.so|
bash|24805|root|mem|REG|8,2|93128|4990790|/lib/x86_64-linux-gnu/libnsl-2.23.so|
bash|24805|root|mem|REG|8,2|35688|4990803|/lib/x86_64-linux-gnu/libnss_compat-2.23.so|
bash|24805|root|mem|REG|8,2|2981280|4854619|/usr/lib/locale/locale-archive|
bash|24805|root|mem|REG|8,2|1868984|4990813|/lib/x86_64-linux-gnu/libc-2.23.so|
bash|24805|root|mem|REG|8,2|14608|4990802|/lib/x86_64-linux-gnu/libdl-2.23.so|
bash|24805|root|mem|REG|8,2|167240|4981342|/lib/x86_64-linux-gnu/libtinfo.so.5.9|
bash|24805|root|mem|REG|8,2|162632|4990791|/lib/x86_64-linux-gnu/ld-2.23.so|
bash|24805|root|mem|REG|8,2|26258|4858348|/usr/lib/x86_64-linux-gnu/gconv/gconv-modules.cache|
bash|24805|root|0u|CHR|136,0|0t0|3|/dev/pts/0|
bash|24805|root|1u|CHR|136,0|0t0|3|/dev/pts/0|
bash|24805|root|2u|CHR|136,0|0t0|3|/dev/pts/0|
bash|24805|root|255u|CHR|136,0|0t0|3|/dev/pts/0|