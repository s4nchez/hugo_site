---
layout: post
title: "Closing the Loop"
date: 2014-12-01T21:00:00+01:00
---
As developers we should be experts in feedback: we want to learn about the consequences of our code changes as quickly as possible. For instance:

* The editor can tell if the new syntax is correct.
* Unit tests can tell if basic logic and interactions are as expected.
* Integration and Acceptance tests can tell how the change will affect the rest of the system.
* Continuous integration can tell if changes coming from different developers will work together.
* Build pipeline can tell if the changed system can be deployed and run after each change.
* Production monitoring can tell if the system is healthy and alert us otherwise.

Those are great techniques for **building things right**, but they don't tell if we are **building the right things**.

For that we should be trying harder to close the feedback loop of **Planning, Building, Measuring and Learning**. So far I've noticed the following approaches have the tendency to help:

* Make sure requirements are created from meaningful conversations ([Impact Mapping](http://www.impactmapping.org))
* Include relevant data gathering into each feature ([How to Measure Anything](http://www.amazon.co.uk/How-Measure-Anything-Intangibles-Business/dp/0470539399)) and make business key performance indicators (KPI) part of the system monitoring
* Use [Retrospectives](http://retrospectivewiki.org/index.php?title=Main_Page) to reflect on the data collected and general KPIs.
* Question any feature about to be built if it doesn't carry a clear purpose.

Unfortunately the most important feedback loop in software development is not purely technical, thus developers should have a more active role trying to make sure the loop is always closed.

I'd be interest to hear what other people are trying on that front.


