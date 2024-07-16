---
date: 2024-07-16
tags:
    -
hubs:
    - "[[Python]]"
urls:
    - https://docs.python.org/3/howto/logging.html
---

# Python_logging 

logging module is a mean of tracking events happening when a software runs.

Accessing logging functionnality via ```logger = getLogger(_name_)``` and calling it's methods.

| Task to perform | Best tool for the task |
| ------------- | --------------  |
| Display console output for ordinary usage  | print() |
| Report events occuring during operation of a program <br> (status monitoring or fault investigation) | info() or debug() |
| Issue a warning regarding a particular runtime event | warnings.warn() in library code if the issue <br> is avoidable and the clien application should be modifiable.<br><br> A logger's warning() if the application can't do nothing about the situation|




