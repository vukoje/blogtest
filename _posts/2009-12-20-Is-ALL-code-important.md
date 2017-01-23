---
layout: post
title:  Is ALL code important?
date:   2009-12-20 12:00:00 +0100
categories: principles
---

Few days ago I saw same ordinary scene on street while going to work that got me thinking... about code off course :) Car driver was complaining to parking service employee about a parking ticket he has just received. He said that he was late for only 15 minutes (parking ticked is valid for 2 hours and drivers are notified with SMS 15 minutes before expiration). At the first moment I taught that 15 minutes isn't that much of a big deal, but then I started thinking what about 20 minutes? Still OK? And 30 minutes? Too much?

![]({{ site.url }}/assets/posts/parking-meter.jpg)

The real question is where to draw the line? Because we obviously can't do this, the right answer is that there should be no tolerance. OK maybe 60 seconds :)

# You said something about code?

Unfortunate driver reminded me about a question I often encounter on my work. **Is all code important? Should really all code follow best coding practices and coding standard?**

Same day I heard that driver complaining, my collage and I asked ourselves if small repeated blocks of code in Unit Test Mock classes are really important?  

If we assume that all code is not important (which will usually happened) you will be constantly wondering where to draw the line between important and not so important code? The answer is same as for parking time overdue, **the line can't be drawn**. You will end up with **universal excuse for having sloppy code**, although you have adopted best practices and maybe you even created a full coding standard.

# But could we have saved time if we could draw the line?

**I think not**. If some code is less important, rarely used, and doing trivial staff, than it's usually easy to implement and hard to get it wrong. This means that code probably won't need any refactoring to enhance its design. I said at my [previous](http://www.vukoje.net/post/2009/11/18/Sinergija-2009-Belgrade.aspx) [two](http://www.vukoje.net/post/2009/10/01/Presentation-Coding-Standard-and-Code-Review.aspx) presentations, and I will say it again, **I can write code by coding standard in same time as if I didn't code by standard**. In fact I can maybe write good code even faster than bad code because I'm already constrained by the standard so I don't have to wonder or think about lowest level solutions (Event design, choosing between Class and Struct etc.).

I hope that this statement provokes you to show that I am no better than you because I know that everyone can write good code with just a little focus and discipline.

**Write good code or find a better excuse**.