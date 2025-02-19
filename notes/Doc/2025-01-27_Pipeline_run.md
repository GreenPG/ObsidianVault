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

A run represents one execution of a pipeline. Both CI and CD pipelines consist of runs. During a run, AP processes the pipeline and agents process one or more [jobs](notes/Doc/2025-01-24_Azure_Pipelines.md#Job), [step](notes/Doc/2025-01-24_Azure_Pipelines.md#Step) and [tasks](notes/Doc/2025-01-24_Azure_Pipelines.md#Task).

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
2. Evaluate dependencies at the [stage](notes/Doc/2025-01-24_Azure_Pipelines.md#Stage) level to pick the first stage to run

For each stage it selects to run, AP:
1. Gathers and validates all job resources for authorization
2. Evaluates dependencies at the job level to pick the first job to run

AP does the following activities for each job it selects to run:
1. Expands YAML strategy: matrix or strategy: parallel multi-configurations into multiple runtime jobs
2. Evaluates conditions to decide whether the job is elligible to run
3. Request an agent for each elligible job

AP checks whether there are new jobs elligible to run as jobs complete. And if there are any more stages as stages complete.

## Agents

### Parallel jobs

AP will adds up all running jobs on all agents and compare that with the number of parallel jobs granted or purchased by your organization.
If there's no available slots, the job has to wait. Once ther is one, the job routes to the appropriate agent type.

### Micrasoft-hosted agents

The Micrasoft-hosted pool is virtually one global pool of machines. Based on the UAML vmImage or Classic editor pool name request, AP selects an agent.
When a job is complete, the running agent is discarded. This way, all agents in Microsoft pool are fresh.

### Self-hosted agents

AP examines the self-hosted pool for compatible agent. Self-hosted agents offer capabilites, indicating that particular software is installed or setting configured.
The pipeline has demands, which are the capabilites required to run the job.

If AP can't find a free agent whose capabilites match the pipeline's demands, the job keep waiting. If there's no agents in the pool whose capabilites match the demands, the job fails.

Self-hosted agents are typically reused from run to run.

## Job preparation

Once an agent accepts a job, it does the following preparation work:
1. downloads all the tasks needed to run the job and chaches them for future use.
2. creates working space on disk to hold the source code, artifacts, and outputs used in the run


## Step execution

Agent runs steps sequentially (new step start only when previous steps has finished or has been skipped).

Steps are implemented by [tasks](notes/Doc/2025-01-24_Azure_Pipelines.md#Task). The task system routes inputs and outputs to the backing scripts.
They also provide common services such as altering system paths and creating new pipeline variables.

Each step runs its own process, isolating its environment from previous steps. This way, environment variables aren't preserved between steps.
Tasks and scripts use logging commands to communicate back to the agent, which takes whatever action the command requests.

## Result reporting and collection

Each steps can report tasks status on the pipeline summary page. Errors and warnings are reporst by marking tasks as succeeded with issues, 
and failures are reports by markings the task as failed. 

The agent can upload [artifacts](notes/Doc/2025-01-24_Azure_Pipelines.md#Artifact) and test results whic are available after the pipeline completes.

## State and conditions

Agent keeps tracks of each step's failure or success. As steps finished, the job's status is updated. Job status always reflects worst outcome from each of its steps.

Before running a steps, the agent checks that step's condition to determine whether it should be run or not.

A `always()` condition can be use to specifiy tasks that needs to be run no matter what else happens.
On the other hand, steps can also be run only on cancellation.


## Timeouts and disconnects

Each job has a timeout. If exceeded, the server cancels the job. It means for the agents to cancal all remaining steps and upload any remaining results.

Jobs have a cancel timeout period in which to complete any cancellation work. Steps can also be marked to run even on cancellation. After a job timeout + a cancel timeout, if the agent doesnt report that work is stopped, the server marks the job as failure.

Agents send a hearbeat message once per minute to the server to confirm that its working. If the server doesnt receive a hearbeat for 5 consecutve minutes, the job is marked as a failure.

## Manage runs through the Azure DevOps CLI

Pipeline runs can be managed using az pipelines runs in Azure DevOps CLI.

- **List pipeline runs**:
```az pipelines runs list```

- **Show pipeline runs details**
```az pipelines runs show```

- **Add tag to pipelin run**
```az pipelines runs tag add```

- **List pipeline run tags**
```az pipelines runs tag list```

- **Delete tag from pipeline run**
```az pipelines runs tag delete```


