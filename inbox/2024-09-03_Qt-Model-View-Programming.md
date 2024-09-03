---
date: 2024-09-03
tags:
    - Doc
hubs:
    - "[[Qt]]"
urls:
    - https://doc.qt.io/qtforpython-5/overviews/model-view-programming.html#model-view-programming
---

# Qt Model View Programming 

Qt contains a set of item view classses that use a model/view architecture to manage relationship between data and the it is presented to the user.
It give greater flexibility to customize the presentation of items and provides standard model interface to allow a wide range of data sources.


## Model/View architecture

Model View Controller (MVC) is a design pattern that consists of three kinds of objects:
- **the Model** is the application object
- **the View** is the the Model screen presentation
- **the Controller** define the way the user interface reacts to user inputs
If thre Model and View objects are combined, it results in the model/view architecture. It separate the way the data is stored from the way it is presented, but provides a simpler
framework. It makes it possible to display the same data in several different views, and implementing new types of view without changing the underlying data structures. 
To allow flexible handling of user input, we introduc the concept of *delegate*. The advantage of having a delegate in this framework is that it allows to customize the way items of data are rendered and edited.
![[Pasted image 20240903170121.png]] 
The model communicates with a source of data, providing an interface for the other components of the architecture.
The nature of the communication depends on the type of data source, and the way the model is implemented.
The view obtains *model indexes*, references to items of data,  from the model. The view can retrive items of data from the source by supplying model indexes to the model.
In standard views, a *delegate* renders the items of data. When an item is edited, the delegate communicates with the model directly using model indexes.

Models, views and delegates communicate with each other using *signals and slots*:
- Signals from the model inform the view about changes to the data held by the data source
- Signals from the view provide information about the user's interaction with the items being displayed
- Signals form the delegate are used editing to tell the model and view about the state of the editor


## Models

All item models are based on **QAbstractItemModel**. It defines an interface used by views and delegate to access data. Data itself does not have to be stored in the model. The provided interface is flexible enough to handle views that represent data
in the form of tables, lists and trees. However, **QAbstractTableModel** and **QAbstractListModel** classes exists for table and list implementations.
Qt provides some ready-made models that can be used to handle items of data:
- **QStringListModel**: store a simple list of QString items
- **QStandardItemModel**: manage more complex tree structures, each of which can contain arbitrary data
- **QFileSysteModel**: provides information aboyt files and directories in the local filing system
- **QSqlQueryModel, QSqlTableModel and QSqlRelationalTableModel**: used to access databases using model/view conventions

## Views

Complete implementations are provide for different kinds of views:
- **QListView**: displays a list of item
- **QTableView**: displays data from a model in a table
- **QTreeView**: display model items of data in a hierarchical list.
This class are all based on **QAbstractItemView** abstract base class.

## Delegates
**QAbstractItemDelegate** is the abstract class for the delegates in the model/view framework. The default implementation is provided by **QStyleItemDelegate**. 

## Sorting

There are two to approaching sorting in the model/view architecture depending of the underlying model:
- if the model is sortable (reimplement sort()), both **QTableView** and **QTreeView** provide an API allowing to sort the model data. You can also enable interactive sorting (sorting by clicking on the view's header), by connectin sortIndicatorChanged() signal to 
sortByColumn() slot.

