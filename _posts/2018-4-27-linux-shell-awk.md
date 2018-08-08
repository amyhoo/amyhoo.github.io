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
```