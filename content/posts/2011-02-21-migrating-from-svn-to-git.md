---
layout: post
date: "2011-02-21 21:10:00"
disquss_thread_id: 43763497
title: "Considering migrating from svn to git?"
category: archive
---
In December last year we decided to migrate our whole codebase from [Subversion](http://subversion.tigris.org/) to [git](http://git-scm.com/). Here is a few tips I'd give to someone considering taking the same route:

**Evaluate the reasons for the migration**. Think about specific scenarios where Subversion is not meeting your project's requirements. Check if too much time is being spent trying to make the current version control work with your workflow. There must be an opportunity to make things simpler or more efficient by switching to git in order to justify the switch.

In our case we were already working almost exclusively with [feature branches](http://martinfowler.com/bliki/FeatureBranch.html), which is a great way to isolate our different pieces of work, but was becoming a hell due to [svn tree conflicts](http://svnbook.red-bean.com/nightly/en/svn.tour.treeconflicts.html). Even though that was the single problem we faced with subversion in years of use, the time wasted with merges lately was enough to justify moving all our code to a more "branch-friendly" system.

**Do your homework**. In other words, before starting anything, learn more about git. The best places to start are probably the [Git Community Book](http://book.git-scm.com/) for theory and [GitHub](https://github.com/) for practice. For me it was really worth learning git's key concepts before moving to practice. It's also a good idea avoiding comparisons with svn until you are comfortable enough with these core concepts. Trying to simply map commands from one tool to another can make life harder, mainly because they don't share the same principles.

**Consider not migrating the whole repository history**. Although the process is not necessarily complicated, it'll probably be time consuming. To give an idea, our 4GB codebase took almost 3 weeks (!) to migrate using [git-svn](http://www.kernel.org/pub/software/scm/git/docs/git-svn.html). That's mainly due to the fact it had to magically create git branches (which are copies of the full repository) from svn branches (generally partial copies). If I had to go through that again today I'd probably migrate trunk only, or even consider starting fresh by splitting our codebase into smaller git repositories and keeping subversion just for reference.

**Spread knowledge before the final switch**. Having the whole team up to speed with the new tool before starting using it on the day-to-day work is a no-brainer. Having a few people willing to train others and help them during the first weeks is also very important to make the transition the less painful as possible.

**Accept the fact all version control systems require discipline**. Don't expect git will solve all the problems in your project. What I noticed is that most of the problems with version control systems start when people get to weird workflows and forget that their work needs to be in a shared repository. Mixing branches, merging wrong content, losing uncommited changes and trashing the local repository will happen regardless of the system. We all make mistakes sometimes and it's best to learn from them instead of cursing the tool.

Now, almost two months later, I can say migrating was a good decision. Branching and merging feel more natural in git, and it has some cool features that are surprisingly useful, like [cherry-picking](http://www.kernel.org/pub/software/scm/git/docs/git-cherry-pick.html). There are still some rare cases when a developer ended up having to recreate a local branch or even having to clone the local repository again, but even these operations are simple enough and I imagine they would probably be avoided if they had more experience with the tool and its workflow.

In any case, just the fact of not having to deal with merge nightmares in subversion again makes me really happy.
