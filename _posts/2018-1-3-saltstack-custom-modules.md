---
categories: software
tags: [devOps] 	
---
# * salt-master
'''
you can develop custom modules under file_roots, you should put your python modules under according directory
'''
## _modules 
those python modules loaded by according salt-master service; there are environment variable defined in salt loader
### \__salt__
```python
def get_grains(*args,**kwargs):
    return __salt__['cmd.script'](grains.items,*args,**kwargs)
```
### \__runners__
### \__proxy__
### \__utils__
## _grains
### \__grains__
## _utils
# * salt-minion