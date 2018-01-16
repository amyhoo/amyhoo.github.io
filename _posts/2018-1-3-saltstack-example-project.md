---
categories: software
tags: [devOps] 	
---
# a project using salt
> there is a project using salt colony to a network of server to support intelligence residence in wide regions

# the abilities
## support cmdb to collection information on minions
## three level structure 
## support web admin interface
## support file distribute

# the structure
![project-structure](/assets/img/salt-wide-region-servers.png)


# desgin
## performance
> * collection data run in small granularity because the data flow traveling on internet
> * using grains to collect information, make module to split grains information into small data

# code
## custom grains
```python
import re
import socket

def master_ip():
	'''
	get master ip address for a minion
	'''
    minion_conf = __salt__['file.read']('/etc/salt/minion')
    m = re.search("[^#]master *: +(.+)", minion_conf)
    host = m.group(1)
    return {'master-ip':socket.gethostbyname(host)}

def minion_ip():
    key,master_ip=master_ip()
    sr=__salt__['network.get_route'](master_ip)
    interface=sr['interface']
    minion_ip = __salt__['network.interface_ip'](interface)
    return {'minion_ip':minion_ip}
```

## custom modules
[reference](https://stackoverflow.com/questions/18360528/how-to-get-ip-address-of-hostname-inside-jinja-template)

```python
# set salt-level as master|syndic|minion
def get_master_ip():
    '''
    get master ip
    :return:
    '''
    salt_level=__grains__.get('salt-level')
    if salt_level == 'master':
        return None
    elif salt_level == 'syndic':
        master_conf = __salt__['file.read']('/etc/salt/master')
        m = re.search("[^#]syndic_master *: +(.+)", master_conf)
        host=m.group(1)
    else:
        host=__grains__.get('master')
    return socket.gethostbyname(host)

def get_minion_ip():
    '''
    get minion ip address
    :return:
    '''
    master_ip = get_master_ip()
    if master_ip:
        sr=__salt__['network.get_route'](master_ip)
        interface=sr['interface']
        minion_ip = __salt__['network.interface_ip'](interface)
        return minion_ip
    else:
        #this is master,get host ip
        links=__salt__['ps.netstat'](':4505')[1]
        for item in links:
            item = item.split()
            if item[-2] == 'ESTABLISHED':
                ip=item[4][:-5]
                return ip
```

# problems
## syn files from master to minion via syndic
```sh
# on salt-syndic machine
apt-get install salt-minion
# on salt-syndic set minion config: master: salt-master
vi /etc/salt/minion
# on salt-syndic set master config: file_roots refer minion cached file_roots
vi /etc/salt/master
# restart service ,make salt-minion to salt-syndic, salt-syndic to salt-master
# now can transfer files
```
