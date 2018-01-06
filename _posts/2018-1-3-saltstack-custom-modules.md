---
categories: software
tags: [devOps] 	
---
# custom modules
## python modules in {file_roots}/_modules 
those python modules loaded by according salt-master service; there are environment variable defined in salt loader 
## use global variable \__grains__,\__salt__,\__utils__
```python
#  __salt__ refer 'salt/modules'
def get_grains(*args,**kwargs):
    return __salt__['cmd.script'](grains.items,*args,**kwargs)
def syn_grains(*args,**kwargs):
    return __salt__['saltutil.sync_grains'](*args,**kwargs)    
def disks():
	# return dictionary
	return __salt__["disk.blkid"]()    
def network():
	# return strings
	return __salt__['cmd.run']('lshw -class network')
# __grains__
def show_grains():
    return __grains__     	
```
## loader salt modules
```python
import salt.config
import salt.loader

__opts__ = salt.config.minion_config('/etc/salt/minion')
__grains__ = salt.loader.grains(__opts__)
__opts__['grains'] = __grains__
__utils__ = salt.loader.utils(__opts__)
__salt__ = salt.loader.minion_mods(__opts__, utils=__utils__)
__salt__['test.ping']()
```
# custom grains
## python modules in {file_roots}/_grains
## import modules
can't import salt modules directly,should import use loader,load order: config,grains,modules

``` python
# use salt.loader to use salt modules
import salt.loader
import salt.config
def is_ping():
    __opts__ = salt.config.minion_config('/etc/salt/minion')
    testmod = salt.loader.raw_mod(__opts__, 'test', None)
    result = testmod['test.ping']()

    return {
        'is_ping': result,
    }
```
## load static custom grains
```python
import yaml
def static_grain():
    with open('/etc/salt/grains', 'rb') as f:
        static_grains = yaml.safe_load(f)
    return {
        'static': static_grains,
    }
```
## _utils
# * salt-minion