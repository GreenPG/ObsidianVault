tags: #Dev #Documentation #ProjectManagement

Sphinx is a solution providing solution to create project documentation using #reStructuredText markup language.
It can produce many outputs formats (HTML, ePub, LaTex, ...)

## Installation 
```
pip install -U sphinx
```

## Document environment initialization

Inside the project directory run ```sphinx-quickstart docs``` to create the basic directory and configuration for the project.

It will create a build directory where rendered doc will be put, Makefiles to simplify Sphinx operations, and a source directory containing conf.py holding the config of the Sphinx project and index.rst that is the root document of the project.
To build the docs, you can run 
```
sphinx-build -M html docs/source docs/build
```
```-M```is the flag to define the output format
```docs/sources```the path to source dir and ```docs/build```the path to target dir.
You can also use ```make Output_Format```which will use default dirs (source/ and build/)

## Automatic documentation

To create documentation, you can use ```autofunction```
