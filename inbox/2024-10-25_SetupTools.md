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


