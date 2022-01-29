---
layout: default
title: DevOps
nav_order: 30
parent: Study
has_children: true
permalink: /docs/study/devops
published: true
---

# DevOps

## What is it?

With the changes and work I'm currently involved in the question of DevOps eventually comes up. When are we no longer just automating SysAdmins/Systems Engineers and DevOps Engineers.
DevOps is a set of practices that bring together software development and operations. Now if you are already writing automation and configuration scripts thats good, but where is your code stored? Are you using centralised Code repository such as Github or Bitbucket, how are you deploying that code at scale?
My current role provides Platform as a Service for clients to use. This has a number of challenges that our department has developed and improved on over the years which I'll explore and articulate to help others navigate this path.

## Challenges

Which tools? Which Processes? Which methodologies?

So to start with you'll have to explore the options of what tools best suit your desired outcome. Are you already using tools or are there tools that your team is already familiar with.
Does your platform or software already have pre-written/developed options so your not having to start from scratch. *Building on top of existing work may save a lot of work to begin with*
When reviewing our needs and capabilities we looked at our existing code base (AWS CloudFormation, Python, PowerShell) and determined that although we currently only deployed in to AWS we would in future be looking to move into other offerings. AWS CloudFormation wouldn't allow this, so we landed on Terraform by Hashicorp. This provided an Infrastructure as Code, single engine and common language to develope and maintain code for any of the current and future Cloud providers. For our Configuration management we had existing Chef code that we wrapped with our custom developed items for deployment, the Chef cookbooks were publicly provided and maintined, we would simply need to add our custom configurations as wrappers to maintain this code. Our deployment of this was using a custom inhouse built deployment tool that would monitor tags of the deployed instances to determine status and run automated scripts (Python/Powershell), the installation would occur using Chef Solo from the local machine.

## Considerations

## Useful links

- [Atlassian - What is DevOps](https://www.atlassian.com/devops/what-is-devops)