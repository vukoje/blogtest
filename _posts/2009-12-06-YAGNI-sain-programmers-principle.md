---
layout: post
title:  YAGNI, sain programmer's principle
date:   2009-12-06 12:00:00 +0100
categories: principles
---

As programmers fight every day with deadline pressures to deliver meaningful software to customers on time, there is one code principle that can speed up and simplify their effort. This principle is called [YAGNI](http://en.wikipedia.org/wiki/YAGNI), which is short for **"You Aren't Going To Need It"**. 

YAGNI is the principle in extreme programming stating that **programmers should not add functionality until it is necessary**, meaning that **you should always implement things when you actually need them, and never when you just foresee that you need them**.

 
![]({{ site.url }}/assets/posts/yagni.png)

The reason for enforcing this principle is that **anticipation in software is very hard** and usually **leads code off track**, while also spending valuable resource - **time**. Anticipation leads to half baked implementation that you maybe didn't need in the first place, and that implementation can turn out to be constraint on implementing some vital functionality that you really need. So what you have is lose-lose situation, you wasted your resources and made situation harder for yourself. 

[Ron Jeffries](http://en.wikipedia.org/wiki/Ron_Jeffries), one of the 3 founders of extreme programming, [said it](http://www.xprogramming.com/Practices/PracNotNeed.html) like this

> Often you will be building some class and you’ll hear yourself saying "We’re going to need...".Resist that impulse, every time. Always implement things when you **actually** need them, never when you just **foresee** that you need them.

> The best way to implement code quickly is to implement less of it. The best way to have fewer bugs is to implement less code.

> You’re *not* gonna need it!

# The art of delaying
 
**Any problem can be solved if you can delay it long enough**, but of course you can't always delay things.

You must remember those situations where Microsoft or some other vendor solved all your problems shortly after you implemented your custom solution. These are really painful moments because usually vendor does it much better than you did and it usually comes free of charge.

Or maybe you remember those painful to implement tasks that altered your core architecture before you found out that they weren't really that important for business and that they will probably be thrown away?

Hart of the justification of YAGNI is that many of these potential needs end up not being needed, or at least not in the way you'd expect. By not doing them until they are really needed you'll save a good deal of effort.

# YAGNI and The Big Design
 
[Jeff Atwood](http://www.codinghorror.com/blog/archives/000021.html) said it like this on his [Coding Horror](http://www.codinghorror.com/blog/archives/000111.html):

> As developers, I think we also tend to be far too optimistic in assessing the generality of our own solutions, and thus we end up building elaborate OOP frameworks around things that may not justify that level of complexity. To combat this urge, I suggest following the YAGNI doctrine. Build what you need as you need it, aggressively refactoring as you go along; don't spend a lot of time planning for grandiose, unknown future scenarios. Good software can evolve into what it will ultimately become.

To make design of your whole big project before you start coding it you need to know/assume most of the requirements. This is the only way you can plan application design that will last for next few years. Reason why YAGNI won't let you create big upfront designs is because they are almost always wrong. They are wrong simply because it is impossible to foresee all user requirements and think of all possible variations of Use Cases and potential design problems. Even if you could do all of this, **requirements will change** before you finish your project. What you should do instead is start from some basic design that will evolve to finally product. Basically you should design a [minimum that works](http://vukoje.net/post/2009/04/08/Do-a-minimum-that-works-%28no-gold-plating%29.aspx), without over engineered grand designs of feature.

If you haven't already, go and read [Martin Fowler's](http://www.martinfowler.com/) article "[Is Design Dead?](http://martinfowler.com/articles/designDead.html#id72716)" that has became manifesto of agile development.

# What about prototypes?
 
YAGNI is in direct conflict with concept of [software prototyping](http://en.wikipedia.org/wiki/Software_prototyping#Throwaway_prototyping "software prototyping"), but the difference is that when you build a prototype you know that you are doing it because you don't know the real requirements (you know that you don't know). This is also why [you should throw away your prototypes](http://www.codinghorror.com/blog/archives/000256.html "you should almost always thow away your prototypes"), or at least evolve them to real code.

Do you have any sad story that could be avoided by YAGNI?
Do you apply YAGNI to your shopping?