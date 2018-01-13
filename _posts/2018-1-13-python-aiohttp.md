---
categories: language
tags: [python]    
---
# client
## example
```python
import asyncio
import aiohttp
import async_timeout
class ReqManager():
    '''
    use aiohttp ,use session which created by " async with aiohttp.ClientSession() as session"
    '''
    def __init__(self):
        self.session = aiohttp.ClientSession()

    async def get(self,url,timeout=10,params={}):
        with async_timeout.timeout(timeout):
            async with self.session.get(url,params=params) as resp:
                text=await resp.text()
                return [resp.status,text]

    async def json(self,url,timeout=10,params={},json={},):
        with async_timeout.timeout(timeout):
            async with self.session.post(url, params=params,json={}) as resp:
                return [resp.status,await resp.text]

    def __del__(self):
        if hasattr(self,'session'):
            self.session.close()

class ReqManagerSSL():

    def __init__(self,verify=False):
        self.session = aiohttp.ClientSession(connector=aiohttp.TCPConnector(verify_ssl=verify))

    async def get(self,url,verify=False,timeout=10,params={}):
        with async_timeout.timeout(timeout):
            async with self.session.get(url,params=params) as resp:
                text=await resp.text()
                return [resp.status,text]

    async def post(self,url,verify=False,timeout=10,params={},data={},):
        with async_timeout.timeout(timeout):
            async with self.session.post(url, params=params,data=data) as resp:
                return [resp.status,await resp.text]

    async def json(self,url,verify=False,timeout=10,params={},json={},):
        with async_timeout.timeout(timeout):
            async with self.session.post(url, params=params,json=json) as resp:
                return [resp.status,await resp.text]

    def __del__(self):
        if hasattr(self,'session'):
            self.session.close()

async def main1():
    req=ReqManagerSSL()
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
# server
