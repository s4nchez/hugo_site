---
layout: post
date: "2009-03-19 19:39:57"
disquss_thread_id: 41421381
title: "Refactoring dojo at Skillsmatter"
category: archive
---
For this dojo, instead of working on a challenge from scratch, we'll start from an existing solution and try to improve it.

The starting point will be the [Minesweeper implementation](http://isanchez.net/2009/03/04/links-and-slides-from-my-session-at-the-software-craftsmanship-2009/) created on a previous coding dojo. It contains only 272 lines of **Java** code (source + tests) and a lot of room for improvement.

Some guidelines for the session:

* Two programmers will work on the code for 7 minutes. After this period, one of them switch his place with someone from the audience.
* The pair decides their next step and make sure the audience understand what they're doing. Discussion with the audience is acceptable, but the final word is always from the pair.
* The pair should follow the [3 Rules of TDD](http://butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd):
 * You are not allowed to write any production code unless it is to make a failing unit test pass.
 * You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.
 * You are not allowed to write any more production code than is sufficient to pass the one failing unit test.
* At the end there will be a retrospective to identify all the lessons learned.

This coding dojo will take place on the 25th March and to participate you need to register at the [session page on the Skillsmatter website](http://skillsmatter.com/event/ajax-ria/coding-dojo-231). If you want to start playing with the code now, it can be downloaded [here](http://isanchez.net/files/codingdojo_swc2009_src.zip).

See you there!
