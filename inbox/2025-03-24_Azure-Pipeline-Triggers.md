---
date: 2025-03-24
tags:
    - Doc
hubs:
    - "[[Azure]]"
    - "[[DevOps]]"
urls:
    - https://learn.microsoft.com/en-us/azure/devops/pipelines/build/triggers?view=azure-devops
---

# Azure Pipeline Triggers 
Triggers can vary based on the type of repo (GH, Azure Repos GIT , Bitbucket...).
We focus here on GH repo.

Trigger are defined at the top of YAML pipeline file with the keyword *trigger:*.

## Branch consideration for triggers in YAML pipelines

| Trigger type | Pipeline YAML version |
|--------------|-----------------------|
| CI triggers (trigger) | The version of the pipeline in the pushed branch is used |
| PR triggers (pr) | The version of the pipeline in the source branch for the PR is used |
| GitHub pull request commen triggers | The version of the pipeline in the source branch for the PR is used |


## CI triggers

CI triggers causes a pipeline to run whenever an update is pushed to the specified branch or specified tags is pushed.

YAML pipelines are configured by deafilt with a CI trigger on all branches, unless the *Disable implied YAML CI trigger* setting is enabled.

### Branches
Which branches get CI triggers can be controlled this way:
```
trigger:
- main
- releases/*
```
You can specify branch full name or a wildcard.
More complex triggers that use *exclude/include* or *batch* need the full syntax:
```
trigger:
    branches:
        include:
        - main
        - releases/*
        exclude:
        - releases/old*
```
If *exclude* is specified without *include*, it's equivalent to specify `include: *`

You can also use the *branches* to specify tags this way:
```
trigger:
    branches:
        include:
        - refs/tags/{tagname}
        exclude:
        - refs/tags/{othertagname}
```

