---
categories: language
tags: [python,java]    
---
# exception
## python 
```python
raise exception from e
```
## java
```java
# e is exception of another type
throw new MyException2(e);
```
# micro-service framework
## java spring-cloud
## python

# iteration
sequence data-structure or a generated by a logic  
## python
1. generator, 
2. iterator,other data-structure can be iterated(list,dict) 
	
## java
1. interface of iterator|iterable(foreach) for collection
2. Stream.generate(iSupplier),Stream.iterate(),Collection.stream()

# Labmda
## java
labmda is an interface; which is deducted by java from context
```java
# f is abstract function of interface of I
Interface I=labmda function f
Runnable r = ()-> {} # but it can be write more neatly in some conditions 
# f is the only abstract function of the params's interface
call(labma f)
# 
```
## python
labmda,an function without name ,used for simple function 

# closure
## java
in java ,the only entity is class,function cannot be embeded in another function.
inner class (the inner instance can refer outside variables and environment). 
but inner class can only use final variable. different with other closure in python or javacript 
## python
function,class both can embeded each other, so closure have many forms

# coroutine
## python
## java
 
# resource operation
## python
```python
with open(filepath) as f:
	print(f.readlines())
```
## java
```java
try( Stream< String > lines = Files.lines( path, StandardCharsets.UTF_8 ) ) {
    lines.onClose().forEach( System.out::println );
}
```
# tools
## python
## java
jdeps analysis the dependency of class
