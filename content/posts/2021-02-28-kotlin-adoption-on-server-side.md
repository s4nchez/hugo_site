---
title: "Reasons Java server-side developers are not adopting Kotlin"
date: 2021-02-28T20:00:00+01:00
toc: false
draft: true
description: The Java server-side hasn't adopted Kotlin heavily yet, and the resistance doesn't always arise from the actual language merits.
---
***TL;DR - What I see in the wild is that Kotlin adoption on the server-side is slow due to a mix of complacency, career self-preservation, and lack of Kotlin visibility. In some specific cases, though, avoiding the adoption is entirely justified.***

It's now almost five years since I wrote my first lines of Kotlin, after using Java for over fifteen years.

Our team didn't follow the typical Java playbook: we used [Utterlyidle] instead of Spring and embraced a Functional Programming approach with [Totallylazy]. We were big fans of IntelliJ and tried to take full advantage of the tooling it provided for Java.

At that time, we were already looking beyond Java. There was some interest in Scala at the time, and we had a few services already written in it. But the complexity,  pain to work alongside a Java codebase, and slow build times made that language unappealing to most of us.

When Google [announced][google-io] Kotlin was becoming an official language for Android development in 2017, another team close to us evaluated the language for their server-side development. Eventually, most of us were giving it a try.

I was blown away by the impact Kotlin had on our codebase. It felt more productive, safer, and the tooling, although not anywhere as mature as Java's, was good enough to make the adoption worth it.

It was also fun to move away from a language that felt old and verbose, and discover what coding styles fit well with Kotlin's features. The excellent interoperability with Java meant that we could rely on the existing ecosystem and transition systems incrementally, without significant disruption to getting things done.

Soon, my interest in Kotlin resulted in co-creating [http4k], a Functional toolkit for Kotlin HTTP applications, and running the [Real World Kotlin Development workshop][rwk] to help other teams attempting to make the same transition.

Eventually, I've left that organisation but was lucky enough to see Kotlin used on the server-side in various other projects. And I also experienced firsthand different people being strongly reluctant to adopt Kotlin for multiple reasons.

It's curious to see that the resistance doesn't always arise from the actual language merits. So why hasn't the Java server-side community adopted Kotlin more heavily?

Here are some reasons my colleagues and I have encountered:

## "We don't have time to learn a new language."

That's a variation of "we can't sharpen our axe because we're too busy chopping trees". It's usually a sign of deeper issues like mounting technical debt and general productivity issues.

Healthy software projects always involve a fair amount of learning. And a competent Java developer can get the basics of Kotlin in hours and will be reasonably productive in days.

A worthwhile investment once the productivity gains kick in when they write simpler code an deal with fewer issues because of the new language.

## "Java is getting better with each release."

That is true: Java is getting better. And releases are coming out faster. On the other hand, it's still miles behind Kotlin in simple things like dealing with nullability.

Maybe the Java community is used to the language's evolution pace. Still, Kotlin provides a way to take advantage of many of those features (and more) in their projects today rather than tomorrow.

## "We are happy as Java developers."

This kind of resistance is the trickiest one. There's not much one can do if a programmer ties their professional identity to a single programming language.

On the one hand, I understand if Java developers don't want to gamble their careers by jumping into a new language's unknown waters. Or they want to be a long-term specialist. And that's fair enough.

On the other hand, I'm yet to see a Java developer "fall behind" because they were using Kotlin. On the contrary, it shows they are continuously looking for the best tool for their jobs, which is a positive trait, at least on the people I help hiring.

## "Kotlin is a hyped language with an unknown future."

That was a common objection we saw around 2017. In that year, Google embraced Kotlin as a first-class language for Android development, reassuring us that big players are interested in the language's longevity.

Today, this is probably less common, given that popular frameworks like [Spring] and [Micronaut] seem to have embraced the new language.

Hopefully, that'll give enough visibility to the language for more server-side people to give it a try.

## "I'm using Eclipse and don't want to switch to IntelliJ."

It's fair to say that the Kotlin experience in Eclipse probably doesn't match JetBrains IDEA.

That's understandable since JetBrains business model includes selling their developer tools. And that's unlikely to change anytime soon.

The only hope for those is Kotlin reaching a critical mass that justifies the further investment in Eclipse support. Until then, the best developer experience for Kotlin developers will remain on JetBrains products.

My very biased view is that IntelliJ is already a better IDE for Java anyway, so it may be worth giving the switch a try too.

## "Kotlin developers are too expensive and hard to come by."

This one is hard to assess: looking at [salary websites][salary], one could conclude that Kotlin salaries are slightly higher overall.

That's a hard comparison to make if we want to consider server-side developers only. In general, that's the Java area that pays the highest, and there's not enough data on the Kotlin side to compare.

Anecdotally, we see in practice that senior Kotlin developers are often the first ones adopting Kotlin, which may give the impression that Kotlin developers are expensive.

On the recruiting side, we haven't seen issues attracting Kotlin developers. We are clear that the job requires the new language and accept that developers will learn it on the job.

That seems to put Java developers at ease and attract those keen to learn new things, which is also a good indicator of potential fit.

## "Kotlin is (already) too complicated."

One of the reasons Kotlin makes for a compelling alternative to languages like Scala is that it struck a decent balance between developer ease of use and advanced features to make operability with Java and adoption by popular frameworks possible.

In practice, this kind of objection tends to be related to the individual team's skills, style, and conventions.

Beginners tend to start writing Kotlin just like they'd write Java. As they get more comfortable with the language, they'll likely push some features (e.g. extensions and inline functions) too far, making the codebase impenetrable to newcomers.

Until a team is fully competent in the new language, we strongly advocate using Boring Kotlin(TM) for as long as possible. Eventually, most of the team will be comfortable enough to find the balance between picking cool language features and making the code accessible to the whole team.

## "It's confusing having two languages in one codebase."

That's a common fear from people who haven't tried Kotlin in a real project.

In practice, as long as the team is on board and mindful that the new Kotlin code needs to co-exist with Java at first, using the two languages in a single project doesn't bring significant pain.

A rule that can help is: "if a change touching the two languages, first start by converting the old code to Kotlin".

That way, the team can avoid a big-bang rewrite and incrementally migrate the areas where they need to add new value.

If some code remains in Java, that's also ok. Most likely, it's because the code works, and there's no pressing need to refactor it.

## "We are more comfortable in Java."

In practice, it may be that a given context doesn't call for the new language. Everything is working fine; the team is getting things done at an acceptable pace and has a good grip on the issue that Kotlin would help address.

In our experience, however, that's the exception and not the rule. More often than not, this kind of resistance originates from a general lack of time or interest in learning rather than a lack of areas to improve.

It's also hard to experience the benefits of Kotlin until trying on a real project, and introducing a new language, even as an experiment, can cause a lot of anxiety.

In those cases, we recommend ["Learning on the Job"][deming] (in the form of coding dojos, brown-bag sessions, etc.) to create a safe environment where this kind of learning can happen.

This approach allows the team to assess both their use of Java and if it's worth investing in Kotlin.

## "I don't see what advantages Kotlin would bring."

Sometimes Java developers are unaware of the language limitations or are too used to them. Other times, they'll dismiss any alternative that makes them question their current language of choice.

Without getting into details, we could say that Kotlin's conciseness and safety are its [main advantages][why-kotlin]. However, some will claim they don't see an issue with Java's verbosity and write safe code already.

It's easy to dismiss Kotlin until you have tried, and when faced with the option, a few people will continue to look for reasons not to try.

----------
Thank you [Uberto Barbini], [Dmitry Kandalov], [David Denton], and Kevin Denver for the ideas for this post.

[Utterlyidle]: https://github.com/bodar/utterlyidle
[Totallylazy]: https://totallylazy.com/
[google-io]: https://blog.jetbrains.com/kotlin/2017/05/kotlin-on-android-now-official/
[http4k]: https://http4k.org
[Spring]: https://spring.io/guides/tutorials/spring-boot-kotlin/
[Micronaut]: https://guides.micronaut.io/creating-your-first-micronaut-app-kotlin/guide/index.html
[salary]: https://www.itjobswatch.co.uk/default.aspx?q=kotlin%2C+java
[rwk]: http://web.archive.org/web/20191105124733/https://skillsmatter.com/courses/602-real-world-kotlin-development-workshop
[why-kotlin]: https://kotlinlang.org/#why-kotlin
[deming]: https://deming.org/institute-training-on-the-job/
[Uberto Barbini]:  https://twitter.com/ramtop
[Dmitry Kandalov]: https://twitter.com/dmitrykandalov
[David Denton]: http://dentondav.id/