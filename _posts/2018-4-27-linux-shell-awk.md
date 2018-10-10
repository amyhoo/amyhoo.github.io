---
categories: os
tags: [linux]  
---
# awk cmd pattern
awk is good at columns
## awk [condition]'{action}' [condition]'{action}' file

```sh
# join two files
awk -F '[=,]' '/egctest.server/ && NR==FNR{split($1,b,".");a[b[2]]=$2;print b[2]}/server/ && NR!=FNR{print $0" "a[$3]":"$2;}' serverinfo.txt egc-appinfo.txt 
awk -F '[=,]'  '/'$env'.server/ && NR==FNR{split($1,b,".");a[b[2]]=$2;}/config-server/ && NR!=FNR{print a[$3];}' $serverfile $appinfofile | xargs

# use variable in awk
awk -v var1="hello" -v var2="world" '{print var1,var2}'
awk '{print ENVIRON["var1"]}'

# also awk can be link with environment var,so you can change awk script with var
awk 'scrpit_part1'$var'script_part2'
```