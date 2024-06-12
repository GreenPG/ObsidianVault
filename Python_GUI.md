---
Title: Python_GUI
Date: 2024-06-11
tags:
  - Dev
  - Python
  - GUI
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
Component of an app are widget. Every widget can be a windows, and a windows can be composed of multiple widget using a layout.

### Signals

Widgets emits signals to inform that something happens.
The receiver of signals are called slots. It can be any function by connecting it to the signal. Many widgets have their own builtins slots
which can be override.
User interaction with the app is an event represented by event object which package up info about what happened.
Events are passed to specifi event handlers on the widget the interaction occured. It is possible to define custom handlers or
extand existing handlers. 
If you create an object inherited of a standard widget to intercept an event, you can still trigger the standard event handler
by using super() inside your overriding method.
ex: 
```
class MainWindow(QMainWindow):
    ...
    def mousePressEvent(self, event):
        print("Mouse pressed!")
        super().mousePressEvent(event)
```

Events are passed to the uppermost widget of the UI. If this widget can't handle the event (or choose not to) the event is then
passed to the parent, all the way up until reaching the main window. An event can be mark as handled by calling the ```accept()``` method, or mark it as unhandled by calling ```ignore()```.


### Multithread application

Qt provides an interface for mutlithreading which is exposed by PySide. It's built around 2 classes: QRunnable, the container of
the work, and QThreadPool, the method which pass the work to alternate threads.

To define a custom runnable, you create a subclass of QRunnable and place you want to execute in the ```run()``` method.
```
from PySide6.QtCore import QRunnable, Slot, QThreadPool

class Worker(QRunnable):

    @Slot()
    def run(self):
        Your code...
```

