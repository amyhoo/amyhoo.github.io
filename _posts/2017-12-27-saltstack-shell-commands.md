---
tags: [python, devOps]
categories: software 	
---
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
salt-run jobs.lookup_jib 'xxx'
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
```