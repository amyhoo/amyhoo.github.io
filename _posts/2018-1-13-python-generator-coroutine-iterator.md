---
categories: language
tags: [python]    
---
# generators
## what is it
### create it using yield sentence
```python
def gene():
	i=100
	while i>0:
		yield i
		i-=1
```
### use generator
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
### compared with functions
1. functions and generator are both used to define a handling procession.
2. function is a process which will start at the init point each time it is called
3. generator also define a process, but it will record last executing point, and will start at that point when called,it is often used to define creation of sequence 

# Coroutines
# what is it
an entity support being called many times; there are many those entities in a thread ,which is managed by a scheduler; those entity can call each other to form a waiting chains.
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