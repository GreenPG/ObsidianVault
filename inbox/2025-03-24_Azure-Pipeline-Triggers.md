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

## Branch consideration for triggers in YAML pipelines

| Trigger type | Pipeline YAML version |
|--------------|-----------------------|
| CI triggers (trigger) | The version of the pipeline in the pushed branch is used |
| PR triggers (pr) | The version of the pipeline in the source branch for the PR is used |
| GitHub pull request commen triggers | The version of the pipeline in the source branch for the PR is used |


