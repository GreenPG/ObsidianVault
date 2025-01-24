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

### Job

### Pipeline

### Run

### Script

### Stage

### Task

### Trigger

