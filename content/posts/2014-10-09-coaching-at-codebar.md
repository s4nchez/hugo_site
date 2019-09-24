---
layout: post
title: "Coaching at codebar.io"
date: 2014-10-09T10:00:00+01:00
---
Last night I had a chance to coach at a [Codebar](http://codebar.io/) event for the first time. They offer free basic programming and web development workshops to people who are underrepresented in the tech industry.

For me it was a great reminder of how difficult it is to learn how to code. Even though my student was following a "getting started" [tutorial](http://tutorials.jumpstartlab.com/projects/ruby_in_100_minutes.html), the amount and complexity of new concepts involved was overwhelming at times. Luckily there were always small rewards (for both of us, mind) when each new concept "clicked" after getting a particular set of commands working.

For example:

```ruby
basket = {"apple" => 3, "banana" => 1}
cities = ["London", "New York"]

puts basket["apple"]
puts cities[0]

cities.each { |city| puts city }

```

Looking at this simple piece of code, there are many syntax concepts we just take for granted:

* The ```[``` and ```]``` can be used to define an Array and to access elements in both Arrays and Hashes.
* Sometimes ```{``` and ```}``` are used to define Hashes. Other times those are actually blocks.
* The ```|city|``` is a parameter to that block, but for methods we define parameters using ```(``` and ```)```.

Even the words I've just used to describe them (access, element, define, parameter, block etc) are a whole new vocabulary to people new to programming. The tutorials do their best to introduce them gently, but there's no escape that programming at the beginning will be challenging. 

I can't remember the last time I had a chance to see someone take their first steps in programming but being there to make their path easier was definitely worth it.

Also, thanks to [Samir](https://twitter.com/samirtalwar) for mentioning it and [despo](https://twitter.com/despo) for organising it. I hope to be able to do it again soon.