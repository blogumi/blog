---
title: Kubernetes, Containers, and Octopus - An Update 
description: A progress update on adding Kubernetes support to Octopus  
author: michael.richardson@octopus.com
visibility: private
published: 2018-07-09
tags:
- Containers
- Docker
---

![Octopus sailing Kubernetes](blogimage-kubernetes-containers-update.png "width=500")

A few months back we asked the Octopus community if they could spare a few minutes and brain-cycles to provide some feedback on our Kubernetes plans.  And you certainly delivered.  So firstly, thank-you!  We sincerely appreciate everyone who shared their thoughts, no matter how strongly we may disagree with them (just kidding).  We're confident it has already resulted in a better product. 

There were a few common themes in the feedback, which caused us to alter course slightly.  We'll talk a little about those, and then finally give a [summary and progress update](#summary).


## #1 A more friendly Kubernetes

![Kubernetes Bear](k8s-bear.png "width=500")

One of the strengths of Octopus has always been that it is user-friendly.  It allowed you to deploy to an ASP.NET website without being a Level 100 IIS Wizard. 

It was pointed out that we were perhaps missing an opportunity to provide a higher level of abstraction; to possibly smooth the learning curve a little. We agreed. 

As part of the first-cut, we are going to include a _Deploy Containers to Kubernetes_ deployment step.  This step will have a richer user-interface, and will walk through the process of:  

- Creating a Kubernetes Deployment, including selecting the deployment-style and the container images 

![Deploy Containers Step - Deployment](deploy-containers-deployment.png "width=500")

- Creating (or updating) the Kubernetes service, including mapping ports

![Deploy Containers Step - Service](deploy-containers-service.png "width=500")

- Configuring Ingress Rules

![Deploy Containers Step - Ingress](deploy-containers-ingress.png "width=500")

The end result (with collapsed sections) will look something like:

![Deploy Containers Step - Final](k8s-deploy-containers-step.png "width=500")


We are excited about this step.  Starting with an empty YAML file, the Kubernetes learning-curve can be daunting, and we feel there is scope for Octopus to help with that. 
We are especially enthused about the ability to select `Blue\Green` as the deployment style.  This will hopefully make some tricky scenarios much easier to configure.  We will talk more about this in future posts. 

## #2 Helm 

So plenty of you really like Helm, huh?  

![Helm Comment](helm-comment.png)

It seems a significant portion of Kubernetes users are using Helm, and many made it clear that not having Helm integration would result in them razing their Octopus installation and salting the server that was hosting it.  Fortunately, once we investigated, Helm actually fits pretty nicely into the Octopus architecture. 

So we are committed to also adding Helm integration. This will be in the form of:

- A Helm Chart Repository feed type

![Helm Chart Feed](helm-chart-repository-feed-type.png "width=500")

- A Helm Deploy Release step 

![Helm Deploy Release Step](helm-deploy-release-step.png "width=500")

We want to provide a great experience whether you use Helm or not. And OK, to be honest, we're a little scared of the Helm militia ;)   

## #3 Not just Kubernetes

We were also reminded that there are many container scenarios which don't involve Kubernetes, and there a few rough edges in Octopus currently for these. For example, deploying container images to ECS. 

To help unlock all the scenarios we won't be adding first-class support for at this moment, we are making a few changes to the family of _Run a Script_ steps to make working with container images a bit nicer. 

Previously, the only way you could reference a package from a script step was to embed the script in the package.  And this wasn't even supported for container images. This meant that working with container images in custom script steps generally involved adding the image tag as a regular variable, and modifying it before creating the release. This works, but it misses the traditional Octopus-goodness around versioning, for example: selecting the package versions when creating a release; being able to bind the release version to the package version; seeing which versions are included in the release; etc. Customers were even simulating these by including dummy packages (e.g. NuGet or Zip) in their deployment process, and using the snap-shotted version of those, which is very clever, but made us sad that they had to jump through those hoops. 

You will now be able to reference packages (including container images) from script steps. The versions of these packages will be selected when creating a release, and will then be available from your custom script, both as a set of variables and the package itself depending on the acquisition options selected (see [the spec](https://github.com/OctopusDeploy/Specs/blob/master/Script-Step-Packages/index.md) for more details). 

This change will apply to the following steps:
- `Run a script` 
- `Run an Azure PowerShell Script` 
- `Run an AWS CLI Script` 
- The new `Run a kubectl Script` step (see below)

We're hopeful this will make container scenarios feel a lot more natural, and will be better able to leverage the power of Octopus. 

## Summary

The first cut of Operation Make-Octopus-Love-Containers will include the following:

- [Kubernetes Cluster deployment target](https://github.com/OctopusDeploy/Specs/blob/master/Kubernetes/index.md#kubernetes-cluster-target)
- [Deploy Containers to Kubernetes deployment step](https://github.com/OctopusDeploy/Specs/blob/master/Kubernetes/index.md#deploy-containers-to-kubernetes-step) 
- [Run a kubectl Script deployment step](https://github.com/OctopusDeploy/Specs/blob/master/Kubernetes/index.md#run-a-kubernetes-script-step) 
- [Helm Chart Repository feed type](https://github.com/OctopusDeploy/Specs/blob/master/Kubernetes/helm.md#helm-chart-feed)
- [Helm Deploy Release deployment step](https://github.com/OctopusDeploy/Specs/blob/master/Kubernetes/helm.md#helm-deploy-release-step)
- [Ability to reference container images (and other packages) from script steps](https://github.com/OctopusDeploy/Specs/blob/master/Script-Step-Packages/index.md)

### When?

Much of the functionality above has been built. We are planning to begin alpha-testing of this in the coming month.  We had many volunteers for being our K8s lab rats, and we are going to reach out to you with the details of how you can play with this very soon.  
