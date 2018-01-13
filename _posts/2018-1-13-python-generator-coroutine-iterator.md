---
categories: language
tags: [python]    
---
# generators
## what is it
a process of creation of sequence, which can be easily use by others.
## create it using yield sentence
```python
def gene():
	i=100
	while i>0:
		yield i
		i-=1
```
## use generator
```python
# in for loops
g=gene()
for i in g:
	print i
	
# or step by step
g=gene()
g.next()
try:
	output=g.next()
	print(output)
except StopIteration:
	pass
```
## compared with functions
1. functions and generator are both used to define a handling procession.
2. function is a process which will start at the initiate point each time it is called
3. generator also define a process, but it will record last executing point, and will start at that point when called,it is often used to define creation of sequence 

# Coroutines
# what is it
coroutine is a procession function, used to create light threads, mainly to cooperate with each other to achieve higher performance . which will wake up others waiting on it when it can run another step. on will sleep when waiting others.
there is scheduler in each thread to coordinate all coroutines in this thread.

## compared with function and generator
1. coroutine , function ,generator are all handling procession. not like object focusing on data, they focus on procession
2. coroutine and generator support being called many times and continue their process on last point.  
3. coroutines have more coordinating relationship each other, and they have a management scheduler implemented by  language itself. coroutines can form a waiting chain and wake up chains.

## compared with thread and process
1. each thread will share time chip, these is no time chip in coroutine, when coroutine sleep,another available one will be executed immediately
2. coroutine will wake up others, or make others sleep , according their dependency. threads will only obey the scheduler. process will waiting for resources, not each other.
3. so thread is a time share mechanism, while process is a resource share mechanism. and coroutine is procession dependency management mechanism

## define a coroutine
```python
#1. recommended after 3.5 version
async def process(item):
    print(item)
#2. or @asyncio.coroutine, use yield from
@asyncio.coroutine
def process(item):
    print(item)  
```
# iterator