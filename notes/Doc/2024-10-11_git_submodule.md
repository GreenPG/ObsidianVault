---
date: 2024-10-11
tags:
  - Doc
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
Is recorded with the `160000`, which is a special mode in Git meaning that its recording a commit as a directory entry rather than a subdir or a file.

## Cloning a Project with submodules

When cloning a project containing submodules, by default you get the directories that contain submodules but none of the files within them yet.
You must then run ```git submodule init``` to initialize your local config file, and ```git submodule update``` to fetch all data from that project and check oyt the appropriate commit listed in the superproject.
Another way is to call ```git clone``` with the ```--recurse-submodules``` flag, or combining the 2 previous command with ```git submodule --init --recursive```

## Working on a project with submodules

### Pulling in upstream changes from the submodule remote

To check for new work in a submodule, you can go into the directory and run ```git fetch``` and ```git merge``` the upstream branch to update the local code.
If you go back at the root of your project and run ```git diff --submodule```, you can see that the submodule was updated and get a list of commits that were added to it.
If you commit at this point you will lock the submodule into having the new code when other people update.
An other way to do it is to run ```git submodule update --remote```. This command will by default assume that you want to update the checkout to the default branch of the remote submodule repo.
You can set this to a diffrent branch if you want by modifying the .gitsubmodules file with ```git config -f .gitmodule submodule.module_name.branch branch_name```. The ```-f``` is to track the changement.

If you want ```git status``` to show a short summary of the changes in the submodule, set the config setting ```status.submodulesummar``` to 1.

By default, Git will try to update all submodules when running ```git submodule --update remote```. To precise a specific submodule, you just have to pass its name to the command.

### Pulling upstream from the project remote

By default, ```git pull``` will fetch the submodules changes but it will not updates them. To finalze the update, you have to run ```git submodule update```.
To be safe you should run it with ```--init```, in case new submodules were added, and ```--recursive```, if any submodule has nested submodules.
To automate this, you can add ```--recurse-submodule```, to ```git pull```, so it will automaticly udpates all submodules.

A special situation is when the upstream repo has change the URL of a submodule in the .gitmodules. In this case, pulling it could fail. To fix this, run ```git submodule sync```


## Working on a Submodule


