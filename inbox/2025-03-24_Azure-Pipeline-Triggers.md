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

To disable trigger, use:
```trigger: none```

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
### Paths
File paths to include/exclude can be specified:
```
trigger:
    branches:
        include:
        - main
        - releases/*
    paths:
        include:
        - docs
        exclude:
        - docs/README.md
```

Wild card are supported for path filters (`*`, `**` or `?`)
- Path are always specified relative to root directory of the repo
- without path filter, root directory of the repo in implicitly included by default
if you exclude a path, you cannot also include it unless you qualify it to a deeper folder.
- path filters order doesn't matter
- paths in Git are case-sensitive.
- variables can't be used in paths, as they are evaluated at run time.

### Tags
Tags can be specified this way:
```
trigger:
    tags:
        include:
        - v2.*
        exclude:
        - v2.0
```

## PR triggers

PR request triggers can be set with the ```pr:``` trigger.

PR triggers follow the same rules as CI trigger for branches and paths.

### Multiple PR updates
You can specify wheter more updates to a PR should cancel in-progress validation runs for the same PR.
The default is *true*
```
pr:
    autoCancel: false
    branches:
        include:
        - main
```
### Draft PR validation

By default, PR triggers fire on draft PR and PR ready for review. To disable PR triggers for draft PR,
set the *drafts* proporty to false
```
pr:
  autoCancel: boolean # indicates whether additional pushes to a PR should cancel in-progress runs for the same PR. Defaults to true
  branches:
    include: [ string ] # branch names which will trigger a build
    exclude: [ string ] # branch names which will not
  paths:
    include: [ string ] # file paths which must match to trigger a build
    exclude: [ string ] # file paths which will not trigger a build
  drafts: boolean # whether to build draft PRs, defaults to true
```

