---
title: "Learning a new codebase from its history beyond the code"
date: 2018-08-20T21:00:00+01:00
draft: false
---
One of the most challenging aspects of learning a new codebase is to understand how things got to be the way they are now. Rather than viewing the current code/documentation as the current representation of reality, I find useful to see them as the result of many internal and external influences over time.

As developers, we tend to see source control as the official history of a codebase. Unfortunately, just looking at the previous commits, no matter how well organised they are, is barely enough to understand the decisions that shaped the system.

A better source of this kind of information is [Architecture Decision Records (ADRs)](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions). When available, those records provide a convenient way to learn about the context where technical decisions were made.

Recently, I’ve been noticing that looking at those is rarely enough. There are clues about the codebase that go undocumented, and the only source is the memory of existing team members. A critical deadline, a strategic mission that eventually changed, a piece of infrastructure that was not particularly reliable, a part of that team that got moved to another country, or an influential team member who left, are all precious information to paint a complete picture of a software project.

Drawing together a timeline a whiteboard with the help of existing team members is an excellent approach to surface some of this history. However, I wish that information was readily available at any given point.

Here are some of the things I wish people documented over time:

* What drove the creation of this project in the first place?
* What was the context of the company at that time?
* Who was in the initial team?
* How has the team structure changed?
* What kind of challenges has the team faced over time?
* What external forces had an impact on the project (positive or negative)?
* Who joined/left the team?
* Who were advocates or champions of specific tools, techniques, and approaches adopted by the team?
* What was the technical context of the original architecture?
* Were there any notable pivots in priorities or goals?

That kind of information exists for any project, and it should be easy to track it as it happens for future reference. And because it’s factual, it does not require to be kept up to date like an architectural diagram.

In the last few days, I’ve been talking to [Nat Pryce](https://twitter.com/natpryce) about some of these ideas, and he came up with [Pottery](https://github.com/npryce/pottery), a tool similar to his [adr-tools](https://github.com/npryce/adr-tools) but intended to “record things that happen in a project”, like an internal Twitter feed. I’m curious to see this kind of approach adopted in the wild and the impact it can have on teams as they evolve.

Ultimately, learning a new codebase from a project history perspective is helpful beyond the technical sphere: it helps us to connect and empathise with the rest of the team and all the challenges that they have faced so far.
