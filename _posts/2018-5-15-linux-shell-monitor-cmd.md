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

<table>
<tr>
<th>进程 等待与阻塞队列</th> <th>虚存/空闲/缓存/文件缓存 </th> <th>虚存读/虚存写 </th><th> 块读/块写 </th> <th>中断ps/切换ps</th><th>用户占比/系统占比/空闲/等cpu</th>
</tr>
<tr>
<th>proc</th> <th>memory </th> <th>swap</th> <th>io</th><th>io</th><th>system</th><th>cpu</th>
<tr>
<td><tr><td>r</td><td>b</td></tr></td>
<td><tr><td>swpd</td><td>free</td><td>buff</td><td>cache</td></tr></td>
<td><tr><td>si</td><td>so</td></tr></td>
<td><tr><td>bi</td><td>bo</td></tr></td>
<td><tr><td>in</td><td>cs</td></tr></td>
<td><tr><td>us</td><td>sy</td><td>id</td><td>wa</td><td>st</td></tr></td>
</tr>
<tr>
<td><tr><td>0</td><td>0</td></tr></td>
<td><tr><td>832</td><td>222808</td><td>139776</td><td>583184</td></tr></td>
<td><tr><td>0</td><td>0</td></tr></td>
<td><tr><td>0</td><td>5</td></tr></td>
<td><tr><td>34</td><td>26</td></tr></td>
<td><tr><td>0</td><td>0</td><td>100</td><td>0</td><td>0</td></tr></td>
</tr>
</tr>
</table>

| 进程队列 | 阻塞队列 | 虚存/空闲/缓存/文件缓存 | 虚存读/虚存写 | 块读/块写 | 中断ps 切换ps | 用户占比/系统占比/空闲/等cpu |
|-----|-----|--------|---------|----------|-------------|------------|
| p wait |p block| m virt | swap | io | system | cpu |
| - | - | - | - | - | - |
|r---b | swpd---free---buff---cache | si---so |   bi---bo  | in---cs | us---sy---id---wa---st |        
| 0---0 | 832---222808---139776---583184 | 0---0 | 0---5 | 34---26 | 0---0---100---0---0 |
                                                                                              
