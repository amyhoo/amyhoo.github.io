---
categories: language
tags: [python]    
---
# combine with thread and process
coroutine is good for io intensive, but coroutine cooperate in one thread. sometimes we need more resource to do more things .like we save data which retrieve from web into files ,database, or make computation .
we need do other things in another thread or process.
## delegate into thread
```python
import asyncio
import time
from concurrent.futures import ThreadPoolExecutor

def logging(x):
   # This is some operation like saving memory on disk
	
asynic def main():
    yield from loop.run_in_executor(t, cpu_bound_operation, 5)

loop = asyncio.get_event_loop()
t = ThreadPoolExecutor(2) 
loop.run_until_complete(main()
```
## delegate into process
[reference](https://stackoverflow.com/questions/28492103/how-to-combine-python-asyncio-with-threads)

```python
# computation instensive,if you transfer data in memory into another process, would use ipc mechanism
import asyncio
import time
from concurrent.futures import ProcessPoolExecutor

def cpu_bound_operation(x):
    time.sleep(x) # This is some operation that is CPU-bound

@asyncio.coroutine
def main():
    # Run cpu_bound_operation in the ProcessPoolExecutor
    # This will make your coroutine block, but won't block
    # the event loop; other coroutines can run in meantime.
    yield from loop.run_in_executor(p, cpu_bound_operation, 5)

loop = asyncio.get_event_loop()
p = ProcessPoolExecutor(2) # Create a ProcessPool with 2 processes
loop.run_until_complete(main()
```
# aiofiles
this won't block thread when operate files
## a architecture about crawler and saving
```python
import aiohttp
import asyncio
asynic crawler()
# get data from web
asyn output()
# save data into files
 
```

# aiohttp
## client
## server
