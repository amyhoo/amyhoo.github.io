---
categories: language
tags: [python] 	
---
# check if  
```python
s="hello there!"
s.startswith('a')
s.endswith('c')
s.isalnum() 
s.isalpha() #是否全是字母，并至少有一个字符 
s.isdigit() #是否全是数字，并至少有一个字符 
s.isspace() #是否全是空白字符，并至少有一个字符 
s.islower() #S中的字母是否全是小写 
s.isupper() #S中的字母是否便是大写 
s.istitle() #S是否是首字母大写的 
```
# char format
```python
s.lower()
s.upper()
s.swapcase()
s.capitalize()
s.title()
```
#width format
```python
width=10
fillchar='*'
s="hello there!"
s.ljust(width,[fillchar]) 
s.rjust(width,[fillchar])
s.center(width, [fillchar]) 
s.zfill(width)
```
#search ,replace
```python
#find
s="hello there!"
substr="th"
start=2
end=5
s.find(substr, start, end) 
s.index(substr,start, end)
s.rindex(substr, start, end) 
s.rfind(substr, start, end) 
s.count(substr, start, end) 
#modify
oldstr='th'
newstr='ht'
count=2
s.replace(oldstr, newstr, count)  
charactor='\n'
s.strip(charactor)  
s.lstrip(charactor) 
s.rstrip(charactor]) 
s.expandtabs(4) #replace tab with 4 space 
```

# split,join
```python
s="hello world!"
sep=','
maxsplit=3
s.split(sep, maxsplit) 
s.rsplit(sep, maxsplit) 
keepends=True
s.splitlines(keepends)
s_list = ["1","2","3"]
','.join(s_list) #把seq代表的序列──字符串序列，用S连接起来
'%s%s%s'%(s_list) 
```

# mapping
```python
from=['a','b','c',',']
to=['A','B','C',';']
table=s.maketrans(from, to) 
deletechars=[';']
S.translate(table,deletechars) 
```
