---
categories: language
tags: [python]    
---
# special char
## `.`
  `.+ `
## *
  \d*
## +
  \w+
## ?
  \w?  
## ()
  \w*(\d+)
## {}
  \d{2}
## ^
  [^abc]
  ^\w+$
## $
  ^\w+$
## |
  [a]|[b]
## `(?P<name>)`
  `(?P<usre>)\w+`
##\<number>
  (\d)abc\1 :1abc1,2abc2,3abc3,etc.
  
# regex expression

## numbers
'\d+'
'[0-9]+'
## not numbers
'\D+'
'[^\d]+'
## space
'\s'
## not space
'\S+'
'[^\s]+'
## char
\w
## not char
\W
[^\w]




# python re module
## match
## search
## finditer
## findall
