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
2. Evaluate dependencies at the [stage](inbox/2025-01-24_Azure_Pipelines.md#Stage) level to pick the first stage to run

For each stage it selects to run, AP:
1. Gathers and validates all job resources for authorization
2. Evaluates dependencies at the job level to pick the first job to run

AP does the following activities for each job it selects to run:
1. Expands YAML strategy: matrix or strategy: parallel multi-configurations into multiple runtime jobs
2. Evaluates conditions to decide whether the job is elligible to run
3. Request an agent for each elligible job

AP checks whether there are new jobs elligible to run as jobs complete. And if there are any more stages as stages complete.

## Parallel jobs

AP will adds up all running jobs on all agents and compare that with the number of parallel jobs granted or purchased by your organization.
If there's no available slots, the job has to wait. Once ther is one, the job routes to the appropriate agent type.

## Micrasoft-hosted agents

The Micrasoft-hosted pool is virtually one global pool of machines. Based on the UAML vmImage or Classic editor pool name request, AP selects an agent.
When a job is complete, the running agent is discarded. This way, all agents in Microsoft pool are fresh.

## Self-hosted agents





