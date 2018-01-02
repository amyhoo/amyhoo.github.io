---
categories: language
tags: [python]    
---
# naming
>## packages
>* lowercase
>* lower_case_with_underscores

>## module
>lower_case_with_underscores
>## c module
>_single_leading_underscore
>## class
>UpperCamelCase
>## function or method
>* lower_case_with_underscores
>* lowerCamelCase

>## variable
>lowerCamelCase
>>### variable available in module
>* _variableName 
>* put the variable into \_\_all\_\_

>>### type variable
>Capitalized_Words_With_Underscores

>## constant
>UPPER_CASE_WITH_UNDERSCORES
>## exception; class name with suffix Error
>UpperCamelCase+Error
>## special naming conventions
>>###  weak "internal use" ;from M import * doesn't import those object; internal class method
>_single_leading_underscore
>>### avoid conflict through inherit; those name will be add class name as prefix
>__double_leading_underscore
>>### magic name
>\_\_double_leading_and_trailing_underscore\_\_
>>### conflict with keyword
>keyword+_

# lay-out
>## using 4 space instead of tab
>## max 79 character in one line
>## two lines between class or function ; one line between method or code block
>## space
>>### using space between operators ,such as = < >
>>### don't use space in other place , such as ["a"]

>## import
>>### don't import more than two module in one line
>>### import order: standard,third party,local 
>>### use absolute import ;explicit relative ;Implicit relative
>>### Wildcard imports is not recommend; from module import *

# comments
>## docstrings for module
```python 
# module doc ; put in the head of module file
"""This is the example module.
This module does stuff.
"""
#
from __future__ import barry_as_FLUFL
#
__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'
#
import os
import sys
```
>## docstrings for class
```python 
# class doc ; following the definition of class
"""
description:
"""
```
>## docstrings for function or method
```python 
# class doc ; following the definition of function or method
"""
description:
params:
return:
"""
```
>## comments for code block
```python 
# add comments before the code block
# Description : etc.
```

# performance
>## string
>>### string concat
>> using ''.join() instead +
>>### using string methods instead of string module
>>''.startswith()  ''.endswith()
>>### check unicode string 
>>isinstance(obj, basestring) in python2

>## compare type
>isinstance(obj, type) instead of type(obj1) is type(obj2)
>## compare None
> using is None,is not None instead of =
>## using def instead lambda
>## derive from Exception instead BaseException

# exception
>## raise exception
```python 
#  recommend
raise ValueError('message') 
# not recommend
raise ValueError, 'message'
```
>## capture exception
```python
# recommend
try:
    process_data()
except Exception as exc:
    raise DataProcessingFailedError(str(exc))
```

>## good try
```python
# yes, limited line in try
try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)   
# no, too much to do in try
try:
    # Too broad!
    return handle_value(collection[key])
except KeyError:
    # Will also catch KeyError raised by handle_value()
    return key_not_found(key)
```