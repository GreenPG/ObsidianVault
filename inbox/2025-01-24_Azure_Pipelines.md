---
date: 2025-01-24
tags:
    - Doc
hubs:
    - "[[DevOps]]"
    - "[[Azure]]"
urls:
    - https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/key-pipelines-concepts?view=azure-devops
---

*Lexique*:
- AP: Azure Pipeline
- CD: [[#Continuous delivery]]
- CI: [[#Continuous integration]] 
- CT: Continuous testing


# Azure_Pipelines 

AP is the part of Azure DevOps that automatically builds, tests and deploys code projects. It combines CI, CT and CD to build, test and deliver code to any destination.
It offers the following benefits:
- works with any language or platform
- deploys to different types of targets at the same time
- integrate with Azure deployments
- builds on Windows, Mac and Linux
- integrates with GitHub
- works with open-source projects

**Languages and applications**
AP can be used for Node.js, Python, Java, PHP, Ruby, C#, C++, Go, XCode, .NET, Android and iOS applications.


## Pipeline basics

A pipeline run sequence follows this sequence:
- a [[#trigger]] tells a pipeline to run
- a [[#pipeline]] is made up of one or more [stages](#Stage). A pipeline can deploy to one or more [environments](#Environment).
- a [[#stage]] is a way of organizing jobs in a pipeline and each stage can have one or more jobs.
- each [[#job]] runs on one [[#agent]]. A job can also be agentless
- each [[#agent]] runs a job that contains one ore more [steps](#Step).
- A [[#step]] canb be a [[#Task]] or [[#Script]] and is the smallest building block of a pipeline
- a [[#task]] is a prepackaged script that performs an action, such as invoking REST API publishing a build artifact.
- an [[#artifact]] is a collection of files or packages published in a [[#run]]


### Agent

An agent computes the infrastructure with installed agent software that runs one job at a time. A pipeline has got at least one job.

### Approvals

Approvals defines a set of validations required befors a deployment runs. Manual approval is a common check performed to control deployments to production environments.
When checks are configured to an environment, a pipeline run pauses until the checks are completed succesfully.

### Artifact

An artifact is a collection of files or packages published by a run. Artifacts are mdae available to subsequent tasks, such as distribution or deployment.

### Continuous delivery

CD is a process by which code is built, tested and deployed to one or more test and production stages. Deploying and testing in multiple stages helpsdrive quality.
CI systems produce deployable artifacts, which include infrastructure and apps. Automated release pipelines consume these artifacts to release new versions and dixes to existing systems. Monitoring and alerting systems run constantly to drive visibilyt into the entire CD process.
This process ensures that errors are caught often and early.

### Continuous integration

CI is the practice used by developement teams to simplify the testing an building of code. CI helps to catch bugs or problems early in the developement cycle, which make them easier and faster to fix.
Automated tests and builds are run as part of the CI process. The process can run on a ste schedule, whenever code is pushed, or both. Items known as artifacts are produced by CI systems. They're used by the continuous delivery release pipelines to drive automatic deployments.

### Environment

An environment is a collection of resources where you deploy your application. One environment can contain one or more virtual machines, containers, web apps, or any service.
Pipelines deploy to one or more environments after a builds is completed and tests are run.

### Job

A stage contains one or more jobs. Each job runs on an agent. A job represents an execution boundary of a set of steps. All of the steps run together on the same agent. Jobs are most userful when you want to run a series of steps in differents environments.

Agentless jobs run in Azure DevOps and Azure DevOps Server without using an agent. A limited number of tasks support agentless jobs.

### Pipeline

A pipeline defines the continuous integration and deployment porcess for your app. It's made up of one or more stages. It can be thought of as a workflow that defines how your test, build and deployment steps are run.
For classic pipelines, a pipeline can also be referred to as a definition.

### Run

### Release

For classc pipelines, a release is a versioned set of artifacts specified in a pipeline. The release includes a snapshot of all the information required to carry out all the tasks and actions in the release pipeline, such as stages, tasks, policies such as triggers and approvers, and the deployment options.
You can create a release manually, with a deployment trigger, or with the REST API.

For YAML pipelines, the build and release stages are in one, multi-stage pipeline.

### Run

A run represents one execution of a pipeline. It collects the logs associated with running the steps and the results of running test. During a run, AP will first process the pipeline and then send the run to one or more agents. Each agent runs jobs. 

For classic pipelines, a build represents one execution of a pipeline.

### Script

A scripts runs code as a step in your pipeline using command line, PowerShell, or Bash. You can write cross-platform scripts for macOS, Linux and Windows. Unlike a [[#task]], a scripts is custom that is specific to your pipeline.

### Stage


### Task

### Trigger

