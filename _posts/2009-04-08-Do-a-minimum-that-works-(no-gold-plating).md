---
layout: post
title:  Do a minimum that works (no gold plating)
date:   2009-04-08 12:00:00 +0100
categories: principles
---

Often when something is being built, the question comes up “How far should we go with this?” If you are building application data access layer, the questions can be:

* How much database vendors should we support?
* How many data types should we support?
* Should caching be integrated automatically?
* Should code support mapping to domain objects?
* Should this mapping support multiple domain objects view of the same system and perform transparent memory synchronization of them?
* What about concurrency control?

![]({{ site.url }}/assets/posts/minimum.jpg)

You could go with all or nothing solution and spend few years building data access layer. This approach is also called [gold plating](http://www.codinghorror.com/blog/archives/000150.html), and is always wrong approach because customers won’t wait 10 years for you to achieve perfection in data access. **The right answer is to do a minimum that works**. In previous example you probably won’t need support for multiple types of database nor advance domain object mapper.

If you do a minimum that works, you have: 

* Satisfied all requirements
* Spent minimum amount of time and money
* You have minimal amount of code/documentation to maintain
* Because you finished faster, feedback will also come faster
* If you were doing a wrong thing, easier it will be to get back on track
* Project leader can do better time estimation if you just build what he requested from you
* You will have more time to work on other things that need more attention

**This is true for code, as it is true for documentation**. If you try to gold plate your requirements you will end up with such amount of documentation that no one will want to read it. Also to much trivial information can hide important information. It is situation when you can’t see forest from trees. Look at [this excellent experiment](http://blog.crisp.se/davidbarnholdt/2009/02/18/1234986060000.html) that shows that you can do more with fewer requirements (Thanks to Vojin for link).

It is important to stress out that doing minimum that works **doesn't imply minimum quality**. I can only think of three situations where low code quality is acceptable:
1. solution is to small for quality to matters (e.g. project shorter than a month).
2. solution is for onetime use and it will be thrown away after (e.g. application for data migration)
3. solution must be finished in unrealistic short period (e.g. to satisfy important client's urgent need) 