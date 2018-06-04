---
categories: language
tags: [python]    
---
# the aim
high performace, accept multi project running paralleling (different processing procedures.) 
accept add task from other process

# framework
## multiple threads prototype
one thread listen ,one thread create multiple coroutine to do tasks.
![crawler1](/assets/img/crawler1.png)   
## one thread prototype
one coroutine listen update tasks event(would execute task_loader to add tasks into queue) ,other multiple coroutine to do tasks. proper high io query ,low compute
![crawler2](/assets/img/crawler2.png)   