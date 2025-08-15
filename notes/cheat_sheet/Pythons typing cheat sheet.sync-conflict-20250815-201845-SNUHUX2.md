---
date: 2024-07-01
tags:
    - cheat_sheet
hubs:
    - "[[Python]]"
urls:
    - https://mypy.readthedocs.io/en/latest/cheat_sheet_py3.html
---
# Built-in types: 
For most types, just use the name of the type in the annotation
Note that mypy can usually infer the type of a variable from its value,
so technically these annotations are redundant
```python
x: int = 1
x: float = 1.0
x: bool = True
x: str = "test"
x: bytes = b"test"
```
For collections on Python 3.9+, the type of the collection item is in brackets
```python
x: list[int] = [1]
x: set[int] = {6, 7}
```

For mappings, we need the types of both keys and values
```python
x: dict[str, float] = {"field": 2.0}  # Python 3.9+
```
For tuples of fixed size, we specify the types of all the elements
```python
x: tuple[int, str, float] = (3, "yes", 7.5)  # Python 3.9+
```
 For tuples of variable size, we use one type and ellipsis
```python
x: tuple[int, ...] = (1, 2, 3)  # Python 3.9+
```

On Python 3.8 and earlier, the name of the collection type is
capitalized, and the type is imported from the 'typing' module
from typing import List, Set, Dict, Tuple
```python
x: List[int] = [1]
x: Set[int] = {6, 7}
x: Dict[str, float] = {"field": 2.0}
x: Tuple[int, str, float] = (3, "yes", 7.5)
x: Tuple[int, ...] = (1, 2, 3)

from typing import Union, Optional

On Python 3.10+, use the | operator when something could be one of a few types
x: list[int | str] = [3, 5, "test", "fun"]  # Python 3.10+
 On earlier versions, use Union
x: list[Union[int, str]] = [3, 5, "test", "fun"]

Use Optional[X] for a value that could be None
Optional[X] is the same as X | None or Union[X, None]
x: Optional[str] = "something" if some_condition() else None
if x is not None:
    # Mypy understands x won't be None here because of the if-statement
    print(x.upper())
If you know a value can never be None due to some logic that mypy doesn't understand, use an assert
assert x is not None
print(x.upper())
```

## Functions
```
from typing import Callable, Iterator, Union, Optional

# This is how you annotate a function definition
def stringify(num: int) -> str:
    return str(num)

# And here's how you specify multiple arguments
def plus(num1: int, num2: int) -> int:
    return num1 + num2

# If a function does not return a value, use None as the return type
# Default value for an argument goes after the type annotation
def show(value: str, excitement: int = 10) -> None:
    print(value + "!" * excitement)

# Note that arguments without a type are dynamically typed (treated as Any)
# and that functions without any annotations are not checked
def untyped(x):
    x.anything() + 1 + "string"  # no errors

# This is how you annotate a callable (function) value
x: Callable[[int, float], float] = f
def register(callback: Callable[[str], int]) -> None: ...

# A generator function that yields ints is secretly just a function that
# returns an iterator of ints, so that's how we annotate it
def gen(n: int) -> Iterator[int]:
    i = 0
    while i < n:
        yield i
        i += 1

# You can of course split a function annotation over multiple lines
def send_email(address: Union[str, list[str]],
               sender: str,
               cc: Optional[list[str]],
               bcc: Optional[list[str]],
               subject: str = '',
               body: Optional[list[str]] = None
               ) -> bool:
    ...

# Mypy understands positional-only and keyword-only arguments
# Positional-only arguments can also be marked by using a name starting with
# two underscores
def quux(x: int, /, *, y: int) -> None:
    pass

quux(3, y=5)  # Ok
quux(3, 5)  # error: Too many positional arguments for "quux"
quux(x=3, y=5)  # error: Unexpected keyword argument "x" for "quux"

# This says each positional arg and each keyword arg is a "str"
def call(self, *args: str, **kwargs: str) -> str:
    reveal_type(args)  # Revealed type is "tuple[str, ...]"
    reveal_type(kwargs)  # Revealed type is "dict[str, str]"
    request = make_request(*args, **kwargs)
    return self.do_api_query(request)

```

## Classes
```
from typing import ClassVar

class BankAccount:
    # The "__init__" method doesn't return anything, so it gets return
    # type "None" just like any other method that doesn't return anything
    def __init__(self, account_name: str, initial_balance: int = 0) -> None:
        # mypy will infer the correct types for these instance variables
        # based on the types of the parameters.
        self.account_name = account_name
        self.balance = initial_balance

    # For instance methods, omit type for "self"
    def deposit(self, amount: int) -> None:
        self.balance += amount

    def withdraw(self, amount: int) -> None:
        self.balance -= amount

# User-defined classes are valid as types in annotations
account: BankAccount = BankAccount("Alice", 400)
def transfer(src: BankAccount, dst: BankAccount, amount: int) -> None:
    src.withdraw(amount)
    dst.deposit(amount)

# Functions that accept BankAccount also accept any subclass of BankAccount!
class AuditedBankAccount(BankAccount):
    # You can optionally declare instance variables in the class body
    audit_log: list[str]

    def __init__(self, account_name: str, initial_balance: int = 0) -> None:
        super().__init__(account_name, initial_balance)
        self.audit_log: list[str] = []

    def deposit(self, amount: int) -> None:
        self.audit_log.append(f"Deposited {amount}")
        self.balance += amount

    def withdraw(self, amount: int) -> None:
        self.audit_log.append(f"Withdrew {amount}")
        self.balance -= amount

audited = AuditedBankAccount("Bob", 300)
transfer(audited, account, 100)  # type checks!

# You can use the ClassVar annotation to declare a class variable
class Car:
    seats: ClassVar[int] = 4
    passengers: ClassVar[list[str]]

# If you want dynamic attributes on your class, have it
# override "__setattr__" or "__getattr__"
class A:
    # This will allow assignment to any A.x, if x is the same type as "value"
    # (use "value: Any" to allow arbitrary types)
    def __setattr__(self, name: str, value: int) -> None: ...

    # This will allow access to any A.x, if x is compatible with the return type
    def __getattr__(self, name: str) -> int: ...

a = A()
a.foo = 42  # Works
a.bar = 'Ex-parrot'  # Fails type checking
```


## Decorators

```
from typing import Callable, TypeVar
from typing_extensions import ParamSpec

P = ParamSpec('P')
T = TypeVar('T')

def printing_decorator(func: Callable[P, T]) -> Callable[P, T]:
    def wrapper(*args: P.args, **kwds: P.kwargs) -> T:
        print("Calling", func)
        return func(*args, **kwds)
    return wrapper
```

Altering signature of the inout functions :
```
from typing import Callable, TypeVar
from typing_extensions import ParamSpec

P = ParamSpec('P')
T = TypeVar('T')

 # We reuse 'P' in the return type, but replace 'T' with 'str'
def stringify(func: Callable[P, T]) -> Callable[P, str]:
    def wrapper(*args: P.args, **kwds: P.kwargs) -> str:
        return str(func(*args, **kwds))
    return wrapper

 @stringify
 def add_forty_two(value: int) -> int:
     return value + 42

 a = add_forty_two(3)
 reveal_type(a)      # Revealed type is "builtins.str"
 add_forty_two('x')  # error: Argument 1 to "add_forty_two" has incompatible type "str"; expected "int"
 ```

Inserting argument:

```python
from typing import Callable, TypeVar
from typing_extensions import Concatenate, ParamSpec

P = ParamSpec('P')
T = TypeVar('T')

def printing_decorator(func: Callable[P, T]) -> Callable[Concatenate[str, P], T]:
    def wrapper(msg: str, /, *args: P.args, **kwds: P.kwargs) -> T:
        print("Calling", func, "with", msg)
        return func(*args, **kwds)
    return wrapper

@printing_decorator
def add_forty_two(value: int) -> int:
    return value + 42

a = add_forty_two('three', 3)
```

