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
