---
date: 2024-08-21
tags:
    -
hubs:
    - "[[Docker]]" 
    - "[[DevOps]]"
urls:
    - https://docs.docker.com/engine/manage-resources/contexts/
---

# Docker contexts 

Docker contexts can be used to manage multiple Docker daemons from a single client.
Each one contain all informations required to manage ressources on the daemon.



## Anatomy of a context

A context is a combination of several properties, including:
- Name and description
- Endpoint configuration
- TLS info

To list available context, you can use the command ```docker context ls```
An asterisk in the NAME column indicates that this is the active context, meaning all docker commands run against this context.
To have more information about a context, you can use ```docker context inspect CONTEXT_NAME```


## Create a context

You can create new context with ```docker context create``` command.
New contexts are stored in a meta.json file below '~/.docker/contexts/' 


## Use a different context

To switch between contexts you can use ```docker context use```.
You can also set the current context using the DOCKER_CONTEXT environment variable. It overides the context set with docker context use.
You can also select context with flag --context.


## Exporting and importing Docker contexts

You can use ```docker context export``` and ```docker context import``` to export and import  contextx on different hosts.
```docker context export``` exports an existing context to a file that can be imported on any hosts that has the docker client installed.
To import this context, you just have to use ```docker context import CONTEXT_NAME EXPORT_FILE```


## Updating a context

```docker context update``` can be used to update fields in an existing context.

