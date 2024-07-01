---
date: 2024-07-01
tags:
    -
hubs:
    - "[[Python]]"
    - "[[DevOps]]"
urls:
    -
---
# Sphinx 
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

To create documentation, you can use ```autofunction``` extensions that will generate automaticly generate docs for your code based 
docstring (for Python).
Include the extension by adding ``'sphinx.ext.autodoc``` in the extensions list of the conf.py files.
Call doc for python object in .rst file by typing
```
.. autofunction:: function_name
```
That works also with class, methods, exception... (auto{object type name})


## CI Integration
Example of GitHub action worklfow file:
```
name: "Sphinx: Render docs"

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
    - uses: actions/checkout@v4             # checkout the code
    - name: Build HTML                      # build HTML documentation using Sphinx
      uses: ammaraskar/sphinx-action@master
    - name: Upload artifacts 
      uses: actions/upload-artifact@v4
      with:
        name: html-docs
        path: docs/build/html/
    - name: Deploy                          # For deploying docs on GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      if: github.ref == 'refs/heads/main'
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: docs/build/html
```

Think to add requirements.txt for Sphinx. 
