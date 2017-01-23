---
layout: post
title:  What to code next?
date:   2009-05-09 12:00:00 +0100
categories: principles
---

When you want to do something, next question always comes up **“What should we do next?”** The answer will differ if you are making decision what module to develop in next few months, or you are wondering what functionality to code next. 

# Choosing next module

![]({{ site.url }}/assets/posts/choice.jpg)

When you pick a development task for a longer period, **always pick the hardest one**. This approach is also called “Swallow the biggest frog first”. This means that if you will be developing some software in period of one year, in first quarter you should tackle all biggest risks and most difficult implementations. These hard problems must be solved before project is completed and if you delay them:
* they will only become harder because already implemented components introduced higher complexity
* you will not have sufficient time to solve them because you already burned big amount of time solving less important issues
* it is more likely that important feedback will come too late when too much time and money is spent 

This approach will lead to [early pain](http://www.martinfowler.com/bliki/EarlyPain.html) in project, where you have large problems right on project start. **You should cherish early pain because alternative is slow and painful project death.**

# Choosing next functionality

When you are choosing next feature the code, **choose the smallest/simplest one that will work**. If you choose simplest possible task, you will be able to:

implement, test and check in your code easily and quickly
you will reduce chances for making a mistake because work is small and simple
you will be less stressed because there will be less things that you have to hold in your head
undo all changes and start from beginning if you get lost or insecure
 
I have stolen this principle from [TDD](http://en.wikipedia.org/wiki/Test-driven_development) and [Refactoring](http://www.refactoring.com/) principles.