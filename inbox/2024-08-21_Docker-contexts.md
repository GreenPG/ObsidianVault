---
date: 2024-08-21
tags:
    -
hubs:
    - "[[Docker]]", "[[DevOps]]"
urls:
    - https://docs.docker.com/engine/manage-resources/contexts/
---

# Docker contexts 

Docker contexts can be used to manage multiple Docker daemons from a single client.
Each one contain all informations required to manage ressources on the daemon.



A context is a combination of several properties, including:
- Name and description
- Endpoint configuration
- TLS info

To list available context, you can use the command ```docker context ls```

