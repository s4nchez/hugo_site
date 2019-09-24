---
layout: post
date: "2009-04-11 19:12:09"
disquss_thread_id: 41421386
title: "Dodging booleans"
category: archive
---
Reading [Mark Needham's post](http://www.markhneedham.com/blog/2009/04/08/coding-passing-booleans-into-methods/) about how inexpressive an API can be when using booleans in method parameters, another clear example came to my mind.

A few weeks ago  we were using a method similar to the following:

```java
public List listUsers(boolean showDisabled);
```
We'd expect that once you call this method passing false, it would return all enabled users and if the parameter is true it included all the disabled users in this list, right? Well, not exactly.

Only when we tried passing true we discovered it actually listed ONLY the disabled users. And unfortunately it was simply impossible to predict this behavior by reading the interface.

What if we used a better representation for this boolean instead?

```java
public enum UserFilter {
    ENABLED_ONLY, DISABLED_ONLY;
}
```

And the interface now would look like:

```java
public List listUsers(UserFilter filter);
```

Notice that I didn't change any behavior, but now it's clear what this method call will return:

```java
myUsers = service.listUsers(UserFilter.ENABLED_ONLY);
```

Besides, if we were really interested in having a list including ALL the users, we could easily extend the filter without having to change the original method or loosing in readability.

The problem with booleans is that they are intentionally inexpressive. They are an essential part of our code when it comes to evaluate conditions and control the flow of execution, but when it comes to define domain-specific concepts, my gut feeling says in most cases they should be avoided.
