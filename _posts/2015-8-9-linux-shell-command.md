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

# tools git
```sh
# store your credentials for repo
git config credential.helper store
git push
```

# compare too array
```
printf "%s\n" ${a1[@]} ${a2[@]} | sort | uniq -u
printf "%s\n" ${a1[@]} ${a2[@]} | sort | uniq -c
```

# dpkg
```sh
# update
apt-get update                  # 更新源  
apt-get upgrade                 # 更新所有已安装的包  
apt-get dist-upgrade                # 发行版升级（如，从10.10到11.04） 

# install
apt-get install <pkg>         # 安装软件包<pkg>，多个软件包用空格隔开  
apt-get install --reinstall <pkg> # 重新安装软件包<pkg>  
apt-get install -f <pkg>          # 修复安装（破损的依赖关系）软件包<pkg>  

# clear /var/cache/apt/archives
apt-get clean 
apt-get autoclean   # only clean packages expired
apt-get autoremove  # clean dependencies don't need anymore
apt-get remove <pkg>          # 删除软件包<pkg>（不包括配置文件）  
apt-get purge <pkg>           # 删除软件包<pkg>（包括配置文件）  

#download
# only download package with dependencies into dir /var/cache/apt/archives 
apt-get -d install XXX
apt-get --download-only install XXX
# download to current dir ,without dependencies
apt-get download xxx
# download source code
apt-get source xxx
apt-get source -d <pkg>  # download and compile it
apt-get build-dep   <pkg> # download and build the environment   

# the packages of software located in /var/debs ,and generate index for apt-get  
dpkg-scanpackages /var/debs  /dev/null  | gzip > /var/debs/Packages.gz
# add it into  sources.list
sed -i 'a deb file:/var debs/' /etc/apt/sources.list

# search 
apt-cache stats             # 显示系统软件包的统计信息  
apt-cache search <keyword>            # 使用关键字pkg搜索软件包  
apt-cache show   <pkg_name>   # 显示软件包pkg_name的详细信息  
apt-cache depends <pkg>       # 查看pkg所依赖的软件包  
apt-cache rdepends <pkg>      # 查看pkg被那些软件包所依赖  
```