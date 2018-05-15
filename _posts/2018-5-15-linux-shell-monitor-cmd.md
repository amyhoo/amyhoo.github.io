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

<table border=0 cellpadding=0 cellspacing=0 width=1224 style='border-collapse:
 collapse;table-layout:fixed;width:918pt'>
 <col width=72 span=17 style='width:54pt'>
 <tr height=18 style='height:13.5pt'>
  <th colspan=2 height=18 class=xl65 width=144 style='height:13.5pt;width:108pt'>进程 等待与阻塞队列</th>
  <th colspan=4 class=xl65 width=288 style='width:216pt'>虚存/空闲/缓存/文件缓存 </th>
  <th colspan=2 class=xl65 width=144 style='width:108pt'>虚存读/虚存写 </th>
  <th colspan=2 class=xl65 width=144 style='width:108pt'>块读/块写</th>
  <th colspan=2 class=xl65 width=144 style='width:108pt'>中断ps/切换ps</th>
  <th colspan=5 class=xl65 width=360 style='width:270pt'>用户占比/系统占比/空闲/等cpu</th>
 </tr>
 <tr height=18 style='height:13.5pt'>
  <td colspan=2 height=18 class=xl65 width=144 style='height:13.5pt;width:108pt'>procs</td>
  <td colspan=4 class=xl65 width=288 style='width:216pt'>memory</td>
  <td colspan=2 class=xl65 width=144 style='width:108pt'>swap</td>
  <td colspan=2 class=xl65 width=144 style='width:108pt'>io</td>
  <td colspan=2 class=xl65 width=144 style='width:108pt'>system</td>
  <td colspan=5 class=xl65 width=360 style='width:270pt'>cpu</td>
 </tr>
 <tr height=18 style='height:13.5pt'>
  <td height=18 style='height:13.5pt'>r</td>
  <td>b</td>
  <td>swpd</td>
  <td>free</td>
  <td>buff</td>
  <td>cache</td>
  <td>si</td>
  <td>so</td>
  <td>bi</td>
  <td>bo</td>
  <td>in</td>
  <td>cs</td>
  <td>us</td>
  <td>sy</td>
  <td>id</td>
  <td>wa</td>
  <td>st</td>
 </tr>
 <tr height=18 style='height:13.5pt'>
  <td height=18 align=right style='height:13.5pt'>0</td>
  <td align=right>0</td>
  <td align=right>832</td>
  <td align=right>222808</td>
  <td align=right>139776</td>
  <td align=right>583184</td>
  <td align=right>0</td>
  <td align=right>0</td>
  <td align=right>0</td>
  <td align=right>5</td>
  <td align=right>34</td>
  <td align=right>26</td>
  <td align=right>0</td>
  <td align=right>0</td>
  <td align=right>100</td>
  <td align=right>0</td>
  <td align=right>0</td>
 </tr>
</table>

| 进程队列 | 阻塞队列 | 虚存/空闲/缓存/文件缓存 | 虚存读/虚存写 | 块读/块写 | 中断ps 切换ps | 用户占比/系统占比/空闲/等cpu |
|-----|-----|--------|---------|----------|-------------|------------|
| p wait |p block| m virt | swap | io | system | cpu |
| - | - | - | - | - | - |
|r---b | swpd---free---buff---cache | si---so |   bi---bo  | in---cs | us---sy---id---wa---st |        
| 0---0 | 832---222808---139776---583184 | 0---0 | 0---5 | 34---26 | 0---0---100---0---0 |
                                                                                              
