---
date: 2025-01-24
tags:
    - Doc
hubs:
    - "[[DevOps]]"
    - "[[Azure]]"
urls:
    - https://app.slack.com/client/T030RLQ4T/C05GUJZTUF3
---

*Lexique*:
- AP: Azure Pipeline
- CD: Continuous delivery 
- CI: Continuous integration
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

### Artifact

### Environment

### Job

### Pipeline

### Run

### Script

### Stage

### Task

### Trigger

