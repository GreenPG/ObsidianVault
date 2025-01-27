---
date: 2025-01-27
tags:
    - Doc
hubs:
    - "[[DevOps]]"
    - "[[Azure]]"
urls:
    - https://learn.microsoft.com/en-us/azure/devops/pipelines/process/runs?view=azure-devops
---

# Pipeline run 

A run represents one execution of a pipeline. Both CI and CD pipelines consist of runs. During a run, AP processes the pipeline and agents process one or more [jobs](inbox/2025-01-24_Azure_Pipelines.md#Job), [step](inbox/2025-01-24_Azure_Pipelines.md#Step) and [tasks](inbox/2025-01-24_Azure_Pipelines.md#Task).

For each run, Azure Pipelines:
- processes the pipeline
- requests one or more agents to run jobs
- hands off jobs to agents and collects the results
For each job, an agent:
- prepares for the job
- runs each step in the job
- reports results


## Pipeline processing

To process a pipeline for a run, AP first:
1. Expands templages and evaluates template expressions
