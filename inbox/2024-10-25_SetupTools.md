---
date: 2024-10-25
tags:
    - #Doc
hubs:
    - "[[Python]]"
urls:
    - https://setuptools.pypa.io/en/latest/userguide
---

# Setuptools 

Setuptools is a Python build backend that can be used to build package through *pip* or *build*.

To use Setuptools as build backend, one must specifying it in the project configuration file (pyproject.toml, setup.cfg or setup.py(deprecated)) by providing a *build-system* section like this:
```
[build-system]
requires = ["setutptools"]
build_backend = "setuptools.build_meta"
```
This must be done in addtion with proper package information about metadat, contents, dependencies .. and package structure.


## Package Discovery and Namespace Packages

Setuptools provide ways to customize which packages should be distributed in in which directory they shoud be found:
```
[tool.setuptools.packges]
find = {} # Scan the project directory with the default parameters
```
Or
```
[tool.setuptools.packages.find]
# All the following settings are optional:
where = ["src"]  # ["."] by default
include = ["mypackage*"]  # ["*"] by default
exclude = ["mypackage.tests*"]  # empty by default
namespaces = false  # true by default
```
With those infos, **setutptools** will walk through directory specified in *where* (default to '.') and filter the packages following the *include* pattern (default to '*'), and then remove packages matchin *exclude* pattern (default to empty).

