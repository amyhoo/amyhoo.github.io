---
categories: language
tags: [java]    
---
# naming conventions
>## class
>UpperCamelCase
>## interface
>UpperCamelCase
>## constant
>UPPER_CASE_WITH_UNDERSCORES
>## variable
>lowerCamelCase
>## method
>lowerCamelCase

# performance conventions
>## do not operate database in loop
>## use StringBuilder's append in loop

# comments conventions
>## file head
```java
//java doc
/**
* copyright etc.
*/
```
>## class | interface
```java
// java doc
/**
/*description:
/*@author:
/*@date:
*/
```
>## constant | variable
```java
// comments
/* user's name */
private String userName;
```

>## method
```java 
// comments
/**
* description：
* @param args1
* @return Xxx
*/

```
>## code block
```java
// comments for single line
/*
comments for mutilple lines
*/
```

#exception
>## log when get a exception
>## don't capture exception in loop 

# security
>## don't show sensitive information
>## avoid resubmit for critical business like order and charge
>## avoid sql injection
>## check parameters from html client
>## CSRF proof
