---
title: Octopus July Release 2018.7
description: Octopus 2018.7 - Sharing the Workload with Workers!
author: rob.pearson@octopus.com
visibility: private
metaImage: metaimage-shipping-2018-7.png
bannerImage: blogimage-shipping-2018-7.png
published: 2018-07-16
tags:
 - New Releases
---

![Octopus Deploy 2018.7 release banner](blogimage-shipping-2018-7.png)

This month, our headline feature is **Octopus Workers** which allows you to shift deployment work off your Octopus Server.  This change brings several benefits including improved security, better performance and other cool things like the ability to create pools of machines dedicated to specific tasks. 

## In This Post

!toc

## Release Tour

<iframe width="560" height="315" src="https://www.youtube.com/embed/tNuYRs_J8cY" frameborder="0" allowfullscreen></iframe>

## Octopus Workers and Worker Pools 

Octopus workers and worker pools allow you to shift deployment work off your Octopus Server. Octopus has always had a built-in worker but we never called it that. Any time you did deployment work that executed a script on the Octopus Server, this was using the built-in worker. This includes Azure and AWS steps as well as scripts steps where you specified to run on the Octopus Server itself.

With the introduction of workers and worker pools, you now have the option to move this work to a separate machine as well as create pools of workers to utilise for special purposes. Nothing has changed about how steps are executed; Workers just provide an option about **where** those steps are executed.

This brings a number of benefits including the following.

* Improved security as custom scripts aren't running on your Octopus Server
* Better performance for your Octopus instance as well as project deployments 
* Other cool stuff like creating worker pools to handle specific tasks like cloud deployments, database deployments and any other special tasks where you may have dependencies that would benefit from a dedicated set of machines. 

Read more about this in our [Octopus Workers blog series](https://octopus.com/blog/tag/Workers).

## Perf and Polish improvements

We’re also shipping some performance and polish improvements. That is, we’ve made some great updates to improve Octopus Server performance and usability. Particularly for larger installations include much lower CPU usage on SQL server in some cases, improvements to deletion and faster project and infrastructure dashboards. We’re continually working to improve our user experience and this month we’ve tweaked the variable snapshot update process as well as improving lifecycle, channel and role scoping pages. 

## Breaking Changes

There are no breaking changes in this release.

## Upgrading

This release contains some optimization for our Machine table that may take some time depending on how many machines you have, so please ensure you allow time for this to complete.

Otherwise, our standard [steps for upgrading Octopus Deploy](https://octopus.com/docs/administration/upgrading) apply. Please see the [release notes](https://octopus.com/downloads/compare?to=2018.7.0) for further information.

## Wrap up

That’s it for this month. Feel free to leave us a comment and let us know what you think! Go forth and deploy!