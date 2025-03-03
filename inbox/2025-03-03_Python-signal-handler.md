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

## Signals and threads

Python signal handlers are always executed in the main Python thread of the main interpreter,
even if the signal was received in another thread. This means that signals can't be used 
as means of inter-thread communication. You can use the synchronization primitives from 
the threading module instead.
Besides, only the main thread interpreter is allowed to set a new signal handler.


## Methods

**signal.signal(*signalnum*, *handler*)**
Set the handler for signal *signalnum* to the function *handler*. *handler* can be a 
callable Python object taking two arguments, or one of the special values signal.SIG_IGN 
or signal.SIG_DFL. The previous signal handler will be returned.
When threads are enabled, this function can only be called from the main thread of the
main interpreter; attempting to call it from other thread will cause a ValueError exception
to be raised.
The *handler* is called with two arguments: the signal number and the current stack frame
(`None` or a frame object).
On Windows, `signal()`can only be called with SIGABRT, SIGFPE, SIGILL, SIGINT, SIGSEGV, 
SIGTERM or SIGBREAK. A ValueError will be raised in any other case. Note that all
systems define the same set of signal names; an AttributeError will be raised if a signal 
is not defined as `SIG*` module level constant.
