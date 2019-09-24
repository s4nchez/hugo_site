---
title: "Deployments vs Releases"
date: 2018-10-30T21:00:00+01:00
draft: false
toc: false
images:
---
When a team is looking to move towards Continuous Delivery, it comes a time when it’s essential to differentiate 
*deployment* from *_release_*.

Traditionally, new versions of the software are built, tested, and made available to users in cycles that vary from 
once every few days to every few months. In that context, each new version will most likely contain some visible 
impact to the user, so the words _release_ and _deployment_ tend to be used interchangeably to express when a new version 
has reached users.

In recent years, however, many development teams have been focusing on reducing the lead time to _deploy_ any given 
change down to hours or even minutes. That has been made possible by increasing the focus on automating most of the 
steps required to verify, assemble and install new versions, as well as increasing the focus on instrumenting and 
monitoring the software so problems can be spotted and fixed quickly.

The ability to _deploy_ new versions of the software more frequently means that often a new version of the software 
doesn’t necessarily contain a visible impact to the user. Those new versions are still worth deploying though, as they 
represent small, valuable increments, and having the latest version of the software being exercised by users earlier 
will:

* Help the team learn how their changes behave in production, where it actually matters.
* Make potential problems (and bugs, in general) easier spot to remediate.
* Exercise the tools and procedures used to build and _deploy_ each version.
* Promote a culture of continuous improvement.

Some examples of small, “invisible” increments that benefit from being deployed as soon as they are ready are security 
patches, performance improvements, or internal changes to make things simpler to evolve or maintain.

Being able to _deploy_ sooner also means the team can take advantage of feature flags to hide incomplete features from 
users until they are ready. During that period, the team may have the ability to enable them for specific users 
(internal or external) to evaluate how it behaves before it can reach a wider audience. The feature can then be 
_released_ with greater confidence and at the most appropriate time.

The splitting of deployment and _release_ may represent a significant shift for those used to longer _release_ cycles. 
The longer the _release_ cycle is, the more significant are the changes, and higher is the chance of things going wrong. 
The natural response, in this case, is to be more reluctant to _deploy_ new changes, especially when the new version 
doesn’t contain something visible to users.

In reality, *deploying more frequently de-risks releasing changes to the users*. That, in addition to the ability to 
better control when and how changes are made available, should make this approach very attractive to modern software 
development teams.