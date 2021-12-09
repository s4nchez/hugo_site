---
title: "App Anatomy: a sociotechnical pattern for continuous delivery infrastructure"
date: 2021-09-25T09:00:00+01:00
toc: true
draft: false
images:
- /images/jump.jpg
description: App Anatomy - a sociotechnical pattern for continuous delivery infrastructure
---
![alt text](/images/anatomy.jpg "Human anatomy illustration")

## Problem

Organisations building multiple applications (services, websites, apps, etc) and adopting Continuous Delivery are required to maintain the infrastructure required to build, configure, and deploy each application.

This _Continuous Delivery Infrastructure_ (CDI) covers aspects such as:
* Continuous Integration (pipeline definitions)
* Deployment Procedures (encoded in pipelines or separate tooling)
* Application/environment configuration for deployment
* Observability & Monitoring (external applications and dashboards)

As the number of applications and teams grow, those should be standardised across the organisation so teams don’t have to reinvent the wheel and good practices can spread.

The organisation at that stage makes a choice (not always deliberate) of who is responsible for maintaining both the standards and the actual infrastructure.

In some cases, a central team is the one creating and maintaining at least part of the CDI for teams. That usually means slower lead times for changes in that area, as creating and updating any aspect of the infrastructure will require coordination with a different team. In return, this team has the opportunity to implement standards and facilitate good practices and reuse across delivery teams.

An alternative approach is letting teams have access to tools and environments so they can set up things the way they need when they need it. This means greater autonomy for teams to evolve their solution and experiment with new approaches. Unfortunately, it means that it becomes less likely teams will approach things similarly, there’s the extra overall effort required by each team, and it’s likely teams will have to learn various lessons the hard way before they get to a good place.

In addition, making sense of this landscape and answering simple questions such as who owns a particular service in production, or has the application been scanned for vulnerabilities also becomes harder and harder depending on the approach chosen.

## Solution

Instead of having teams creating their own CDI solutions, or a centralised team responsible for each application’s CDI individually, the App Anatomy pattern is based on a central framework maintained by a platform team plus controlled autonomy for delivery teams.

This is achieved with four elements:

#### 1. Conventions for various application elements.

Conventions are defined to eliminate unnecessary deviation and the need for extra tooling.

For instance, the application name may be the directory name of where it lives in the source control system. The name of the pipeline in the continuous integration system will also use the same name. Same thing for names of dashboards that are automatically managed.

These conventions are enforced by software and encode what the organisation considers good practice.

Other examples are:
* Each application needs a README and CONTACT file with certain content in them.
* All applications are built by calling a `build` script (which can delegate to language-specific building tools).
* A service gets deployed to an environment if all tests pass and no manual gatekeeping mechanism is defined.

#### 2. Definition of an application descriptor (a.k.a. app anatomy)

Not all things can be derived from convention when different teams have different needs, and that's where the app anatomy information (coming from statics file or output from hook script) comes in.

It allows defining extra parameters used to define the CDI for a particular application.

The app anatomy contains important application details such as:
* Required dependencies (libraries or other services)
* Where the application should be deployed and whether manual approval is required
* Configuration variants (per environment in case of services, or per different builds of mobile apps)
* Extra resources needed (domain names, databases, static assets)
* Where test results and other build reports can be found
* What’s the team that currently maintains the application 
* Exceptions to the conventions (e.g. different service name)

Those bits of information (plus conventions) are used to drive the creation and maintenance of all infrastructure to build, deploy, and operate the application.

#### 3. Central automation tooling (a.k.a. auto pipeline)

Once conventions and other metadata are available in source control for each application, central automation tooling will monitor changes and apply them to the CDI.

This tool (or set of tools) is responsible for the automation of tasks that teams (delivery or central) would manually normally perform such as defining build pipeline or configuring deployment parameters.

Another common responsibility of this central tooling is to act as the repository of information about what applications are being developed, by whom, and how.

#### 4. Secondary tools for information radiation and wider organisation use

With central automation in place, it becomes possible to create documentation that by definition won’t get out-of-date over time. It also allows building more specialised reporting around topics the organisation may care about such as testing approach or security metrics.

Depending on the design of the automation tooling, it can also be extended by other teams from the organisation to perform relevant tasks such as alerting when a particular service gets deployed to production or automatically running business-specific post-deployment tasks.

## Consequences

The main consequence of this pattern is that it allows organisations to find their sweet spot between giving teams autonomy and having (self-enforcing) standards in place.

This approach reduces development efforts for teams, as they don’t have to jump into infrastructure code every time they need to create or update the CDI for a particular application. Instead, they can leverage previous knowledge about the conventions and tooling to focus on business challenges rather than technical details.

For the wider organisation, a benefit of this approach is automated governance of their applications. Because CDI is managed by central tooling, it becomes easier to inspect everything being built and deployed and collect all sorts of useful information such as ownership details and inter-dependencies.

Another organisational benefit is that app anatomy reduces friction for engineers to move between teams.

Unsurprisingly, this pattern doesn’t come for free, and there are some trade-offs that need to be taken into account.

The main one is that App Anatomy requires investment. Organisations have very specific requirements when it comes to building and deploying applications, and finding suitable off-the-shelf solutions for App Anatomy is extremely difficult.

There are solutions that follow a similar approach for part of the application lifecycle (Heroku and Travis being notable examples) and those are good to get started but are also limited for those wanting to unlock the full potential of this approach.

By requiring internal development it also means App Anatomy is a solution that doesn’t get built overnight. It requires a group of people dedicated to understanding what good looks like for the organisation. This team also needs to be able to work with teams to encode and document the right conventions, as well as support teams during the transition to this approach.

Finally, there are also ongoing costs to maintain such a solution. Most organisations will benefit from iterating on their solution, and keep educating new teams and individuals on the approach. Also, App Anatomy tooling itself requires infrastructure to run.

Still, for organisations trying to scale their Continuous Delivery capabilities, the benefits of App Anatomy are likely to outweigh these costs over time, as it reduces the variance of solutions to the same problem and unlocks building solutions that all teams (and the organisation as a whole) can benefit at once.

## Background

I've first come across this pattern at a large scientific publisher in London. 

Although the origins of the "app anatomy" name and pattern are unclear, the implementation led by [Steve Freeman](https://twitter.com/sf105), [Ivan Moore](https://twitter.com/ivanrmoore), and a small "tools engineering" team made dozens of teams extremely effective at shipping high-quality software to production quickly and with low friction.

There's a [talk](https://skillsmatter.com/skillscasts/6925-a-meta-pipeline-for-generating-continuous-delivery-pipelines-for-microservices) by [Hilverd Reker](https://twitter.com/hilverd) and [Steve Freeman](https://twitter.com/sf105) that goes into more details of that particular implementation and provides a good taste of this pattern in practice.

Thank you [Ivan Moore](https://twitter.com/ivanrmoore), [Nat Pryce](https://twitter.com/natpryce), [Matt Savage](https://twitter.com/savagematt), [David Denton](https://twitter.com/tarkaTheRotter), and [James Shiell](https://twitter.com/jshiell) for the various conversations around this topic and input for this article.

---
Photo from Joyce McCown via [unsplash](https://unsplash.com/photos/IG96K_HiDk0)
