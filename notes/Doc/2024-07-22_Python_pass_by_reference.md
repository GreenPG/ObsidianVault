---
date: 2024-07-22
tags:
    - Doc
hubs:
    - "[[Python]]"
urls:
    - https://realpython.com/python-pass-by-reference/
---

# Python_pass_by_reference 

## Pass by Reference vs Pass by value

Pass by reference means that the argument you're providing to a function is a reference to a variable that already existe in memory,
rather than an independent copy of its value. 
This way, all operations performed on this reference will directly be applied to wich it refers.

In opposite, when passing by value, you only pass an independent copy of the original values of the variable to the function.


## Pass by assignement

Python use a 3rd method wich is pass by assignement. That is when you call a function, each function argument becomes a variable to which the passed value is assigned.

### Assignement in Python

If the assignement target is an identifer, or variable name, then this name is bound to the object. Every variable is a name bound to an object. 
If the name is already bound to a separate object, then it's rebound to the new object.
The structure in which all Python objects are implemented has a counter, the reference counter,  that keep tracks of how many names have been bound to this object.

## Best practices to replicate Pass by reference in Python

### Return and Assign

For function returning single value:
```
def square(n):
    return n * n

x = 4

x = square(4)
print(x)
# 16
```

For function operating on multiple values:
```
def greet(name, counter):
    return f"Hi, {name}8", counter + 1

counter = 0

greeting, counter = greet("Alice", counter)
# greeting = "Hi, Alice!"
# counter = 1
```

### Use Objects Attributes

In Python, if the target of an assignement is an object's attribute that support assignement, 
then the object will be asked to perform the assignement on that attribute. So if the object is pass an an argument to a function, its attribute can be modified in place.

```
from types import SimpleNamespace

ns = SimpleNamespace()

def square(instance):
    instance.n *= instance.n

ns.n = 4
square(ns)
# ns.n = 16
```

### Use Dictionaries and List


