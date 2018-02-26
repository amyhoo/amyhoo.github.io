---
categories: language
tags: [python]    
---
# aim
I would like to build a framework of task management easily persistent and flexible for all kinds of work.
a task have only uuid to identify themselves. what a task really do depended upon their own attributes. a task
have three phase in their life-cycle, created by loader, executed by executor,and saved by saver. each phase are independent, so can be adept to all kinds work. the three phase are process and assembled by a procession.

and I use tasks to manage web fetching because I would like to make sure  each fetching activity 's success

# task_handler
```python
# -*- coding: utf-8 -*-
'''
this module is used to manage tasks with TaskHandler
task is an entity or record with at least attributes :
    uuid : identify a typical task
    other attributes based on what kind of task it is
task can be inited with init attributes, and then to be handled ,updated with more attribute
such as add more running information or result of task.and then be saved ,and relative information
collected into database.
here ,task information stored into nametuple

TaskHandler use task information to do work. there are many kind of TaskHandler, include:
    loader: loader information from files and init task information
    executor: do work with task information
    saver: collect information from task
all TaskHandler have a generator to get a sequence of task

'''
import csv
import collections
import uuid
import asyncio
import aiofiles


class BaseTaskHandler(object):
    '''
    three kind handler:
        loader
        executor
        saver
    '''

    def __init__(self,*args,**kwargs):
        '''
        task class
        '''
        self.task_class = None


class TaskLoader():
    '''
    loader task from files or else
    '''

    def __init__(self):
        super(TaskLoader,self).__init__()
        self._tasks=[]
        self._fields=None

    def tasks(self):
        '''
        generator offer a sequence of tasks
        mark sure task contain uuid attribute
        '''
        yield from self._tasks


class TaskLoaderCsv(TaskLoader):
    '''
    loader task from csv file with fields' name
    filename: csv file store task information with fields' name
    uuid_fields: used to generate only uuid
    '''

    def __init__(self,filename,uuid_fields=[]):
        super(TaskLoaderCsv, self).__init__()

        with open(filename) as filer:
            reader = csv.DictReader(filer)
            self._fields=reader.fieldnames

            if 'uuid' not in self._fields:
                self._fields.append('uuid')
                self.task_class = collections.namedtuple('Task', self._fields)
                self._tasks = [self.task_class(**self.gen_task(uuid_fields,row)) for row in reader]
            else:
                self.task_class = collections.namedtuple('Task', self._fields)
                self._tasks = [self.task_class(**row) for row in reader]

    def gen_task(self, uuid_fields,record_dict):
        '''
        generate uuid for record_dict with uuid_fields
        '''
        name=''.join([record_dict[field] for field in uuid_fields])
        id=uuid.uuid3(uuid.NAMESPACE_URL,name)
        record_dict['uuid']=str(id)
        return record_dict


class TaskSaver(BaseTaskHandler):
    '''
    save tasks into files
    '''

    def __init__(self,task_class,filename,flush_max=1000):
        super(TaskSaver, self).__init__()
        self.task_class = task_class
        self._output = filename
        self._flush_max = flush_max
        self._task_buffer = []

    def formatter(self):
        '''
        format the self_task
        '''
        return self._task_buffer
    
    async def flush(self):
            async with aiofiles.open(self._output, mode='a') as filer:
                writer = csv.DictWriter(filer,self.task_class._fields)
                await writer.writerows(self.formatter())
            self._task_buffer=[]

    async def save_task(self,task,**kwargs):
        '''
        add other informtion into task ,and save it into file
        '''
        task_info=task._asdict()
        task_info.update(kwargs)
        self._task_buffer.append(task_info)
        if len(self._task_buffer) > self._flush_max:
            await self.flush()

class TaskProcession(BaseTaskHandler):
    '''
    assemble each step of task, loader, saver, executor
    '''

    def __init__(self,loader,executor,saver):
        '''
        loader: TaskLoader
        '''
        super(TaskProcession, self).__init__()
        self.loader = loader
        self.task_class = loader.task_class
        self.saver = saver
        self.executor = executor

    def run(self):
        loop = asyncio.get_event_loop()
        tasks = self.loader.tasks()
        task_list= [self.execute(task) for task in tasks]
        loop.run_until_complete(asyncio.wait(task_list))

    async def execute(self,task):
        '''
        '''
        resp = await self.executor.do_task(task)
        await self.saver.save_task(task,**resp)

    def tasks(self):
        yield from self.loader.tasks

if __name__=='__main__':
    loader= TaskLoaderCsv('test.csv',['url'])
    saver = TaskSaver(loader.task_class,'filename')
    from tasks.task_executor import TaskWebExecuter
    executor = TaskWebExecuter(loader.task_class)
    process = TaskProcession(loader,executor,saver)
    process.run()
```

# task_executors
use task process to do web fetching

```python
from tasks.task_handler import  BaseTaskHandler
from webclient.web_client import ReqManager

class TaskWebExecuter(ReqManager,BaseTaskHandler):
    '''
    this executor do web fetch
    '''

    def __init__(self,task_class, protocol='http', *args, **kwargs):
        super(TaskWebExecuter,self).__init__(protocol='http', *args, **kwargs)
        self.task_class = task_class
        if 'url' not in self.task_class._fields :
            raise ("the web task should have url attribute")

    async def do_task(self, task):
        url = task.url
        if 'params' not in self.task_class._fields:
            params = {}
        else:
            params = task.params
        if 'data' not in self.task_class._fields:
            data ={}
        else:
            data = task.data
        if 'method' not in self.task_class._fields:
            method = 'get'
        else:
            method = task.method

        if method == 'get':
            resp = await self.get(task.url, params=params)
        elif method == 'post':
            resp = await self.post(task.url, params=params, data=data)
        elif method == 'json':
            resp = await self.json(task.url, params=params, json=data)
        else:
            resp = None
        return resp
```

# web client use asyncio mechanism
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
            		text = await resp.text()
                return {status:resp.status, text: resp.text}

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