---
date: 2025-03-03
tags:
    - Doc
hubs:
    - "[[Python]]"
urls:
    - https://docs.python.org/3/library/signal.html
---

# Python signal handler 

Custom signal handlers can be created using the signal.signal() function.

Some defaults handlers are already defined:
- SIGPIPE is ignored
- SIGINT is translated into a KeyboardInterrupt exception

A handler for a particular signal remains installed until it is explicitly reset, with 
the exception for SIGCHLD, which follow the underlying implementation.

## Execution of Python signal handlers

A Python signal handler does not get executed inside the low-level (C) signal handler. 
Instead, the low-level signal handler sets a flag which tell the virtual machine to 
execute the corresponding Python signal handler at a later point. This has consequences:
- it makes little sense to catch synchronous errors like SIGFPE or SIGSEGV that are 
  caused by an invalid operation in C code. Python will return from the signal handler 
  to the C code, which is likely to raise the same signal again, causing Python to 
  apparently hang.
- a long-running calculation implemented purely in C may run uninterrupted for an 
  arbitrary amount of time, regardless of any signals received. The Python signal
  handlers will be called when the calculation finishes.
- if the handler raises an exception, it will be raised 'out of thin air' in the main 
  thread.


