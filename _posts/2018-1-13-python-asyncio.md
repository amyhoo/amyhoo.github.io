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
### example
```python

__version__ = '0.2'
__author__ = 'AmyHoo'

import asyncio
import aiohttp
import async_timeout


class ReqManager():
    '''
    use aiohttp ,use session which created by " async with aiohttp.ClientSession() as session"
    '''

    def __init__(self, protocol='http', *args, **kwargs):
        '''
        args: verify:false|true,
        kwargs: verify:false|true
        '''
        if 'verify' in kwargs:
            verify = kwargs.get('verify')
        else :
            verify=args[0] if args else False
            
        if protocol == 'https':
            self.session = aiohttp.ClientSession(connector=aiohttp.TCPConnector(verify_ssl=verify))
        else:
            self.session = aiohttp.ClientSession()

    async def get(self, url, timeout=10, params={}):
        with async_timeout.timeout(timeout):
            async with self.session.get(url, params=params) as resp:
                text = await resp.text()
                return [resp.status, text]

    async def post(self, url, verify=False, timeout=10, params={}, data={}, ):
        with async_timeout.timeout(timeout):
            async with self.session.post(url, params=params, data=data) as resp:
                return [resp.status, await resp.text]

    async def json(self, url, timeout=10, params={}, json={}, ):
        with async_timeout.timeout(timeout):
            async with self.session.post(url, params=params, json={}) as resp:
                return [resp.status, await resp.text]

    def __del__(self):
        if hasattr(self, 'session'):
            self.session.close()

async def main1():
    req=ReqManager(protocol='https')
    resp=await req.get('https://www.baidu.com/')
    print (resp)

async def main2():
    req=ReqManager()
    resp=await req.get('http://www.baidu.com/')
    print (resp)

if __name__=="__main__":
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main1())
    loop.run_until_complete(main2())
    loop.close()

```
## server
