---
layout: default
title: Infrastructure as Code
nav_order: 10
parent: DevOps
#has_children: true
permalink: /docs/study/devops/iac
published: true
---

# Infrastructure As Code

## What is it?

Infrastructure As Code is the deployment, configuration and management of Infrastructure components (Network, Servers, firewalls, etc) using code. 
Most Cloud providers have a native available implementation of this, for example; AWS has CloudFormation, and Azure has Azure Resource Manager. 
Traditionally you would have started out testing on your preferred Cloud provider using the Portal or Console, this is traditionally referred to as ClickOps and its a great way to get familir with the tools and offerings. However when you decide to standardise or offer a service at scale you are going to find a number of problems trying to achieve this via the console.

## Challenges

Depending which product you choose you'll have to ensure that the code is stored and shared amongst you're team. Storing this in a Version Control System such as Github or Bitbucket will track changes, history and allow collaborative development. There are a number of additional benefits depending on the tool that you choose, including branching, CICD, actions and third party integrations.

Thats getting a little ahead of ourselves, lets look at the products available.

Terraform, Ansible, CloudFormation, Azure Resource management, Puppet, Pulumi....
Regardless of your choice you should ensure that you maintain and adopt strict adherance to using the tool. Failure to commit to this will result in Drift, you've put all this time and effort to codifying your architecture only to have someone come along and 'fix' something quickly in the console. You then decide to commit another change to the code and this ends up undoing those manual changes.
Essentially we are talking about Desired State, this is central to both Infrastructure as Code and Configuration Management. Its the concept where you construct and configure a codified solution using a declaratative approach, based on a specification or statement of work. And in order to maintain and improve that desired state you should ensure that all of your changes or fixes are completed in code to maintain that state.

## Advantages

There are a few obvious advantages to using IAC including standardisation, speed of deployment, decreased downtime and reduced costs. Standardisation helps ensure that if you are deploying multiple solutions or environments you can support and maintain them knowing that they are in a known configuration. This follows on to speed of deployment, having a tested and standard build will ensure you can quickly deploy and redeploy Infrastructure.
Reducing costs are a two fold benefit, by not spending time deploying and fixing issues ensures operational hours are not wasted reworking the same problems by preventing human error.

## Disadvantages

Total commitment to a standard and complete agreement to only use DevOps practices to maintain moving forward. This doesnt appear on the face of it to be a disadvange however it relies on a team that is in agreement and adherance moving forward. Training will make this easier barrier to entry for existing staff however the descision of those who don't wish to work in this new way will nneed to be redirected to other areas or moved on all together.

## Other Considerations

When an operations team seeks to adopt these new practices you are in essence doubling your workload. You now not only need to deploy and configure the same servers. You now need to maintain a code base, and work on automation of the other areas.
Depending on how work arrives and requests are raised you may need to adopt a software development practice such as Agile or Kaban to plan and manage the mainenance of the new code.

## Useful links

[Microsoft Infrastructure as Code](https://docs.microsoft.com/en-us/dotnet/architecture/cloud-native/infrastructure-as-code)
[Top10 Infrastructure As Code tools 2021](https://docs.microsoft.com/en-us/dotnet/architecture/cloud-native/infrastructure-as-code)