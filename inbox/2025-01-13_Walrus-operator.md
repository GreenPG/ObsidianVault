---
date: 2025-01-13
tags:
    - Doc 
hubs:
    - "[[Python]]"
urls:
    - https://realpython.com/python-walrus-operator/
---

# Walrus operator 

The assignment expression operator, or walrus operator (:=) allows to assign values to variables as part of an expression. i.e. combining assignment and evaluation in a single statement.

It's an operator used in assignment expressions which can return the value being assigned unlike traditional statements.
There's no identical code where both assignment statement using - and assignment expression using := would be valid.


## Use cases

**Debugging**

When trying to debug complex expressions, you can use the walrus operator to give a name to subexpression and keep its value:
Example:
For the following expressions
```
2 * rad * asin(
    sqrt(
        sin((ϕ2 - ϕ1) / 2) ** 2 + cos(ϕ1) * cos(ϕ2) * sin((λ2 - λ1) / 2) ** 2       
    )
)
```
you can isolate the first part of square root expression like this:
```
2 * rad * asin(
    sqrt(
        (ϕ_hav := sin((ϕ2 - ϕ1) / 2) ** 2)
        + cos(ϕ1) * cos(ϕ2) * sin((λ2 - λ1) / 2) ** 2       
    )
)
```
This way you can calculate the whole expression and keep track of the value of ϕ_hav at the same time.

**List and Dictionaries**
The walrus operator can be used to avoid multiple calls to function to initialize lists or dictionaries.
Example:
```
numbers = [2, 4 ,5, 0, 1, 9, 7]

description = {
    "length": len(numbers),
    "sum": sum(numbers),
    "meadn": sum(numbers) / len(numbers),
}
```
can be written like this:
```
numbers = [2, 4 ,5, 0, 1, 9, 7]

description = {
    "length": (num_length := len(numbers)),
    "sum": (num_sum := sum(numbers)),
    "meadn": num_sum / num_len,
}
```


**List Comprehension**
It can be used to avoid calling expensive functions multiple times and still use list comprehension.
example:
`results = [slow(num) for num in numbers if slow(num) > 0]`
become:
`results = [value for num in numbers if (value: slow(num)) > 0]`
