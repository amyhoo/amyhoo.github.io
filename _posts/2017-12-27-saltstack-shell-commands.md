---
tags: [python, devOps]
categories: software 	
---
# grains

## ls items
>		@master# salt '*' grains.ls

## all items
>		@master# salt '*' grains.items

## get litems
>		@master# salt '*' grains.item 'xxx'
>		@master# salt '*' grains.get 'xxx'

## update grains which defined in /etc/salt/grains
>		@master# salt '*' saltutil.refresh_modules

## sync _grains modules
>		@master# salt '*' state.highstate
>		@master# salt '*' saltutil.sync_grains
>		@master# salt '*' saltutil.sync_all

## 