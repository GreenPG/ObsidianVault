---
date: 2024-07-16
tags:
    - Doc
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
| ERROR | Due to a more serious problem, the software has not been able to perform some function |
| CRITICAL | A serious error, indicating that the program itself mat be unable to continue running | 

Default level is WARNING. A logger will track only the event that are at its level or above.
With the debaut level, only WARING, ERROR and CRITICAL event will be tracked.
If you call loggign methods directly (without creating a logger), they will basicConfig() if it has not been called yet.

# basicConfig()

The basicConfig() method can be used to configure a bunch of feature of logging. It must be called before any logging method if you want this config to be applied.

## Logging to a file
You precise a file to record your logs providing a file path with the `pathname` parameter, or just a file name to `filename` parameter. The encodage can be precise with they `encoding` parameter.
```logging.basicConfig(filename='file_path', encoding='encodage)```

## Logging variable data
logging use the old %-style string formatting for backwards compatibility.

## Changing format of displayed messages

basicConfig() provide a format attribute to precise the format to display logs. All attribute to format string can be found here :https://docs.python.org/3/library/logging.html#logrecord-attributes.
ex :
```
logging.basicConfig(format='%(levelname)s:%(message)s')
logging.warning("This message should appear on the console")

#output
WARNING:This message should appear on the console
```

