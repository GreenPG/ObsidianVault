---
Title: Python_GUI
Date: 2024-06-11
tags: #Dev #Python #GUI
---

# Python_GUI 

## Qt

Qt is a cross-platform framework for creating GUI. It runs on all major desktop platforms and mobile or embedded platforms, 
and still providing native-looking interface.

The core of every Qt application is the QApplication widget (unique for every app) which hold the event loop of the app.
Each interaction with the app generates an event which is place in the event queue. In the loop, 
the queue is checked at each iteration and passed the first event in the queue to a specific event handler, which deal with it 
and pass the control back to the loop.


## PySide6

Base on Qt like PyQt. Major difference is the licence. GPL for PyQt and LGPL for PySide.


