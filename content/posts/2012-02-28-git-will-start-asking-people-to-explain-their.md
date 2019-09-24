---
layout: post
date: "2012-02-28 22:01:02"
disquss_thread_id: 106082350
title: "Git will start asking people to explain their merges. Finally!"
category: archive
---
Annoyed by too many pointless merges in your git history? So [here's some good news for you](http://git-blame.blogspot.com/2012/02/anticipating-git-1710.html):

> [...] in 1.7.10 and later, the git merge command [...] will open an editor before creating a commit to record the merge result, to give the user a chance to explain the merge, just like the git commit command the user runs after resolving a conflicted merge already does.

My hope is that this simple change will make people start thinking twice before merging, instead of just doing it because git makes it easy. And I'm glad the git team and I share the same vision about the subject:

> [...] Merging updated upstream into your work-in-progress topic without having a good reason is generally considered a bad practice. Such a merge in the wrong direction should be done only when it is absolutely necessary, e.g. your work-in-progress needs to take advantage of recent advancement made on the upstream.  Otherwise, your topic branch will stop being about any particular topic but just a garbage heap that absorbs commits from many sources [...]

Apparently that was a design mistake from the early days of git, for which [Linus also adds his point of view](https://plus.google.com/102150693225130002912/posts/SrePhcj6XJe):

> [...] if you don't like explaining your merges, this might be annoying. Of course, if you don't explain your merges, you are annoying, so it all evens out in the end. "Karmic balance", so to say.


 
