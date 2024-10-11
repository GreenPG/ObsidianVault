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
By default, submodules will add the subproject into a directory of the same name. You can add a diffrent path at the end of the command to put elsewhere.
It will also create a .gitmodules file if it doesn't exist. It stores the mapping between the project's URL and the local subdirectory.

Git sees the newly created subdirectory as a submodule and doesn't track its contents when you're not in it. Instead, Git sees it as a particular commit from that repo.
Is recorded with the `160000`
