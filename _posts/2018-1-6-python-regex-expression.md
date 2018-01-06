---
categories: language
tags: [python]    
---
# special char
```python
# .
'.+' 
# *
'\d*'
# +
'\w+'
# ?
'\w?'  
# ()
'\w*(\d+)'
# {}
'\d{2}'
# ^
'[^abc]'
'^\w+$'
# $
'^\w+$'
# |
'[a]|[b]'
# (?P<name>)
'(?P<usre>)\w+'
# \<number>
'(\d)abc\1' : ['1abc1','2abc2','3abc3',]
```
  
# regex expression
```python
# numbers
'\d+'
'[0-9]+'
# not numbers
'\D+'
'[^\d]+'
# space
'\s'
# not space
'\S+'
'[^\s]+'
# char
'\w'
# not char
'\W'
'[^\w]'
```

# python re module
## compile
```python
import re
pattern = re.compile(r'\d+')
m=pattern.search('(98233)ad(983834)')
if m:
    print(m.groups()) # all groups
    print(m.group(0)) # the whole matched string
    print(m.group(1)) # the first group
    print(m.group(2)) # the second group
    print(m.group(1,2)) # the first the second group
```
## match
only match from the first char
## search
in the string 
## finditer
return an iterator,which will generate all matching strings
## findall
return all matched strings
## sub
## subn
## split