---
tags: [python, devOps]
categories: software 	
---
# params 
## tgt
```sh
# normal with wildcard
salt '*' test.ping
# ip
salt -S '192.168.1.101' test.ping
# regex
salt -E 'web.+' test.ping
# grains
salt -G 'os:Ubuntu' test.ping 
# support list
salt -L 'minion1,minion2' test.ping
# combine many way 
salt -C 'web* or S@192.168.*' test.ping
```
# grains

## ls items
```sh
# ls items
salt '*' grains.ls
# all items
salt '*' grains.items
# get items
salt '*' grains.item 'xxx'
salt '*' grains.get 'xxx'
```

## update grains which defined in /etc/salt/grains
```sh
salt '*' saltutil.refresh_modules
```
## sync _grains modules
```sh
salt '*' state.highstate
salt '*' saltutil.sync_grains
salt '*' saltutil.sync_all
salt '*' saltutil.sync_modules
salt '*' state.apply
```

# job
```sh
salt --async '*' test.ping
salt -v '*' test.ping
salt-run jobs.list_jobs
salt-run jobs.lookup_jid 'xxx'
salt-run jobs.last_run target=nodename function='cmd.run'
```
# shell cmd
```sh
salt '*' 'cmd.run' 'whoami'
```

# hardware check
## disks
```sh
#show all phsical disks
salt '*' grains.get disks
#show physical and logic disk information
salt '*' status.diskstats
salt '*' status.diskusage
#logic disks
salt '*' disk.blkid
#get information of a particular physical disk
salt '*' disk.hdparms
#get usage of volumes
salt '*' disk.usage
```
## net adapter
```sh
# show physical net adapter
salt '*' grains.get hwaddr_interfaces
# show netdev 
salt '*' status.netdev
salt '*' status.netstats
salt '*' network.get_bufsize
salt '*' network.calc_net
salt '*' network.hw_addr
salt '*' network.netstat
# show subnet
salt '*' network.subnets
salt '*' network.interface
salt '*' network.routes
salt '*' network.default_route
salt '*' network.get_hostname 
salt '*' network.get_route
salt '*' dnsutil.A hostname
```

# find packages
```sh
salt '*' pkg.search python
salt '*' pkg.info_installed python
salt '*' pkg.list_pkgs
```

# keys
```sh
# list 
salt-key -l salt-minion
# list all
salt-key -L
# accept
salt-key -a salt-minion
# accept all
salt-key -A
# reject
salt-key -r salt-minion
# reject all
salt-key -R
# delete 
salt-key -d salt-minioin
# delete all
salt-key -D
# print fingerprints
salt-key -f salt-minion
# print all fingerprints
salt-key -F 
```

# file
```
# transfer below size of max_event_size of file: 1m
salt-cp '*' file1,file2,file3,DEST
```