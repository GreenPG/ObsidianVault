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


### Models

All item models are based on **QAbstractItemModel**. It defines an interface used by views and delegate to access data. Data itself does not have to be stored in the model. The provided interface is flexible enough to handle views that represent data
in the form of tables, lists and trees. However, **QAbstractTableModel** and **QAbstractListModel** classes exists for table and list implementations.
Qt provides some ready-made models that can be used to handle items of data:
- **QStringListModel**: store a simple list of QString items
- **QStandardItemModel**: manage more complex tree structures, each of which can contain arbitrary data
- **QFileSysteModel**: provides information aboyt files and directories in the local filing system
- **QSqlQueryModel, QSqlTableModel and QSqlRelationalTableModel**: used to access databases using model/view conventions

### Views

Complete implementations are provide for different kinds of views:
- **QListView**: displays a list of item
- **QTableView**: displays data from a model in a table
- **QTreeView**: display model items of data in a hierarchical list.
This class are all based on **QAbstractItemView** abstract base class.

### Delegates
**QAbstractItemDelegate** is the abstract class for the delegates in the model/view framework. The default implementation is provided by **QStyleItemDelegate**. 

### Sorting

There are two to approaching sorting in the model/view architecture depending of the underlying model:
- if the model is sortable (reimplement sort()), both **QTableView** and **QTreeView** provide an API allowing to sort the model data. You can also enable interactive sorting (sorting by clicking on the view's header), by connectin sortIndicatorChanged() signal to 
sortByColumn() slot.
- if the doesn't have the required interface or you want to use a list view to present your data, you can use a proxy model to transform the structure of your model before presenting the data in the view.

### Convenience classes

There are some *convenience* classes derived from the standard view classes for the benefit of applications that rely on Qt's item-based view and table classes. They are not intended to be subclassed.
Ex: **QListWidget**, **QTreeWidget**, **QTableWidget**
These classes are less flexible than the view classes, and cannot be used with arbitrary models. It's recommende to use a model/view approach to handling data in item views unless you really need an item-based set of classes.
If you want to take advantage of the model/view architecture while still using an item-based interface, consider using view classes (**QListView**, **QTableView** or **QTreeView) with **QStandardItemModel**.


## Using Models and Views

### Two models included in Qt

**QStandardItemModel** and **QFileSysteModel** are the 2 standards models provided by Qt. 
- **QStandardItemModel**: multipurpose model used to represent various data structures needed by list, table and tree views. It holds the items of data.
- **QFileSysteModel**: maintain information about the contents of a directory. Does not hold any data, simply represents files and directories on the local file system.

### Model classes

#### Basic concepts

In model/view architecture, model provides a standard interface that views and delegates use to access data. The standard interface is designed by **QAbstractItemModel** class. No matter how the items of data are stored in the underlying data structure, 
all subclasses of **QAbstractItemModel** represent the data as a hierarchical structure containing table of items. This convention is used by views to access items of data in the model. 
![[Pasted image 20240903174657.png]]

Models also notify any attached views about changes to data through the signals and slots mechanism.

#### Model indexes

*model index* represent a piece of information that can be obtained via a model. View and delegates use these indexes to request items of data to display.
Only the model needs to know how to obtain the data, and the type of data managed by the model can be defined fairly generally. 
Model indexes contain a pointer to the model that created them, preventing confusion when working with more than one model.

Since models may reorganize their internal structure from time to time, model indexes are only temporary references and should not be stored. If a long-term reference to a piece of information is needed, a *persistent model index* must be created.
This index is keeped up to date by the model. **QModelIndex** provide temporary indexes and **QPersistentModelIndex** provides persistent indexes.

To obtain a model index, three properties must be specified to the model: a row number, a column number and the model parent of the index.


#### Rows and columns

Data from a model can be accessde as a simple table in which items are located by their row and column numbers. 


#### Parents of items

The table-like interface provided by models is ideal when using data in a table or list view. However, structure such as tree views require the model to expose a more flexible interface.
As a result, each item can be the parent of another table of items.
When requesting an index for a model item, we must provide some information about the item's parent.

#### Item roles 
Items in a model can perform various *roles* for other components, allowing different kinds of data to be supplide for differnet situations.
We can ask the model for item's data by passing it the model index corresponding to the item, and by specifying a role to obtain the type of data we want.
More common uses for item data are covered by the standard roles definied in **ItemDataRole**.

#### Summary

- Model indexes give views and delegates information aboyt the location of items provided by models in a way that is independant of any underlying data structures
- Items are referred to by theur row and column numbers, and by the model index of theiur parent items.
- Model indexes are constructed by models at the request of other components, such as views and delegates
- If a valid model index is specified for the parent item when an index is requested using index(), the idenx returned refers to an item beneath the parent item in the model. The index obtained refers to a child of that item
- If an invalid model index is specified for the parent item when an index is requested using index(), the index refers to a top-level item in the model
- the **role** distinguishes between the different kinds of data associated with an item.

### View classes

#### Concept

View obtains items of data from the model and presents them to the user. The way these datas are presented does not need to ressemble to the representation of the data provided by the model, and *may be completly different*.

The separation of content and presentation is achieved by the use of a standard model interface provided by **QAbstractItemModel**, a standard view interface provided byt **QAbstractItemView**, and the use of model indexes that represent items of data in a general way.
Views typically manage the overall layout of the data obtained from models. They may render individual items of data themselves, or use delegates to handle both rendering and editing features.

Views also handle navigation between items, and some aspects of item selection. It also implement basic user interface features, such as context menus and drag and drop. A view can provide default editing facilities for items, or it may work with a delegate to provide
a custom editor.


