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
To execute this runnable in another thread, you have to create an instance of QThreadPool and pass your runnable to it.
```
threadpool = QThreadPool()
worker = Worker()
threadpool.start(worker)
```
You can pass arguments to your runner via the init method. It even give the possibility to pass the function to execute and
then creating a generic runner who can execute any function.
```
class Worker(QRunnable):
    '''
    :param callback: The function to run on this worker thread.
    :type callback: function
    :param args: Arguments to pass to the callback function
    :param kwargs: Keywords to pass to the callback function
    '''

    def __init__(self, callback, *args, **kwargs):
        super(Worker, self).__init__()

        self.callback = callback
        self.args = args
        self.kwargs = kwargs

    @Slot()
    def run(self):
        self.fn(*self.args, **self.kwargs)
```

#### Thread IO
You can use At signal and slot framework to pass data and state from running workers to main thread in a thread-safe way.
Signal can ```.emit``` values which are picked up by slots which have been previously linked with ```.connect```.

```
import traceback, sys

class WorkerSignals(QObject):
    '''
    Defines the signals available from a running worker thread.

    Supported signals are:

    finished
        No data

    error
        tuple (exctype, value, traceback.format_exc() )

    result
        object data returned from processing, anything

    '''
    finished = Signal()  # QtCore.Signal
    error = Signal(tuple)
    result = Signal(object)

class Worker(QRunnable):
    '''
    Worker thread

    Inherits from QRunnable to handler worker thread setup, signals and wrap-up.

    :param callback: The function callback to run on this worker thread. Supplied args and
                     kwargs will be passed through to the runner.
    :type callback: function
    :param args: Arguments to pass to the callback function
    :param kwargs: Keywords to pass to the callback function

    '''

    def __init__(self, fn, *args, **kwargs):
        super(Worker, self).__init__()
        # Store constructor arguments (re-used for processing)
        self.fn = fn
        self.args = args
        self.kwargs = kwargs
        self.signals = WorkerSignals()

    @Slot()  # QtCore.Slot
    def run(self):
        '''
        Initialise the runner function with passed args, kwargs.
        '''

        # Retrieve args/kwargs here; and fire processing using them
        try:
            result = self.fn(
                *self.args, **self.kwargs
                status=self.signals.status
                progress=self.signals.progress
            )
        except:
            traceback.print_exc()
            exctype, value = sys.exc_info()[:2]
            self.signals.error.emit((exctype, value, traceback.format_exc()))
        else:
            self.signals.result.emit(result)  # Return the result of the processing
        finally:
            self.signals.finished.emit()  # Done

    def execute_this_fn(self):
        for n in range(0, 5):
            time.sleep(1)
        return "Done."

    def print_output(self, s):
        print(s)

    def thread_complete(self):
        print("THREAD COMPLETE!")

    def oh_no(self):
        # Pass the function to execute
        worker = Worker(self.execute_this_fn) # Any other args, kwargs are passed to the run function
        worker.signals.result.connect(self.print_output)
        worker.signals.finished.connect(self.thread_complete)

        # Execute
        self.threadpool.start(worker)

```


### QtDesigner

A software that provide an interface do design a Qt GUI by drag and drop. Each widget UI is defined in a .ui file.
You can then import it with PySide either by directly loading it from .ui file:
```
from PySide6 import QtCore, QtGui, QtWidget
from PySide6.QtUiTools import QUiLoader

loader = QUiLoader()

#Function that allow to apply modification to the loaded widget
def mainwindow_setup(w):
    w.setWindowTitle("Main Window")

app = QtWidget.QApplication(sys.argv)

window = loader.load("mainwindow.ui", None) # The second argument is the parent of the widget
mainwindow_setup(window)
window.show()
app.exec()
```
Or by convert it to Python and then import it to your app. You can convert by using the CLI command pyside6-uic:
```pyside6-uic mainwindow.ui -o MainWindow.py```
And then import it like this:
```
from MainWindow import Ui_MainWindow

class MainWindow(QtWidgets.QMainWindow, Ui_MainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.setupUi(self)

app = QtWidgets.QApplication(sys.argv)

window = MainWindow()
window.show()
app.exec()
```
