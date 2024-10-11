---
date: 2024-10-11
tags:
    - #Doc
hubs:
    - "[[git]]"
urls:
    - https://git-scm.com/book/en/v2/Git-Tools-Submodules
---

# git_submodule 

Problem: working on a project that need to use one or many other project from within. You want to be able to treat those projects as separate yet still be able to use one from within another.

Git solution are submodules. They allow to keep a Git repo as a subdirectory of another git repo. You can clone a repo into another one and keep commits separated.

## Starting with submodules

To add a submodule, use ```git submodule add``` with the absolute or relative URL of the project you like to start tracking.
