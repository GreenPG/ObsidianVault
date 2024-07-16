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
| Report an error regarding a particular runtime event | Raise an exception |
| Report suppression of an error without raising an exception | A logger's error(), exception() or critical() method appropriate to the specific error and application domain |

The logger methods are named after the level of severity  of the events they are used to track:

| Level | When it's used  |
| ------------- | -------------- | -------------- |
| DEBUG | Detailed information, typically of itnerst onlywhen diagnosing problems | 
| INFO | Confirmation that things are working as expected | 
| WARNING | An indication that something unexpected happened, or indicative of some problem in the near future. The software is stil working as expected| 
| ERROR | Due to a more serious problem that the program itself may be unable to continue running| 
| CRITICAL | A serious error, indicating that the program itself mat be unable to continue running | 


