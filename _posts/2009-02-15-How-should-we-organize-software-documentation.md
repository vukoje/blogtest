---
layout: post
title:  How should we organize software documentation?
date:   2009-02-15 12:00:00 +0100
categories: software documentation
---

In my [previous blog post](/post/2008/12/23/Should-software-be-documented.aspx) I've said something about the **reasons** of documenting software. Now the question is how to do it? People don't like to write documentation, documentation is often hard to find and maintain and it is usually obsolete. We need to organize documentation in such way that it is **meaningful**, **easy to maintain**, **easy to find** and **hard to become obsolete**. You can say that right solution is somewhere between full bureaucracy and anarchy.

![]({{ site.url }}/assets/posts/documentation.jpg)

# Process oriented solution

Some people believe that with detailed organization and business processes they can completely controls their business. This approach is something like **programming humans** that are executed by business process. In this environment programmer would have to follow exact documenting process and typically fill big documentation templates with concrete information. This procedure can guarantee that people will **avoid documenting** at all costs and it doesn't guarantee that information populated in templates will be useful enough. It may give away false impression of fully controlling this vital activity but in practice it isn't so.

Programmers dislike (hate) writing software documentation because it **is not interesting and creative**. If they are further more crippled by heavy formal process, programmers will do what ever they can just to finish that part of work by filling templates with low quality and incomplete information.

**If it is not easy for programmer to find and update some information he simply won’t do it** (if he is not explicitly asked to do it). As software evolves and knowledge of the real system increases, documentation becomes obsolete because programmers are not updating it. After enough time has passed you are faced with **massive obsolete documentation** that in the end of the day is making more harm than good because you can never know if information is accurate.  

![]({{ site.url }}/assets/posts/words.jpg)

# People oriented solution 

My opinion is that company **Wiki site** (e.g. [ScrewTurn Wiki](http://www.screwturn.eu/) )is much better solution for knowledge base than bunch of populated word templates resting on some server's file system. Pages on Wiki site are **easier to search**, **easier to alter** and they can **automatically notify** all participants when documentation changes. This approach can seam frightening to management because everyone can alter any document they want. In general, employees shouldn't be constrained in their work so that they can not make mistake. **Not being able to make mistake means that you aren't doing any creative work and that you should be replaced with machine.** Instead, company should introduce quality checks for activities that are more likely to introduce an error or where error can be very expensive. Some dedicated person (e.g. project leader) could inspect all documentation incremental changes in previous weak and verify them. Bear in mind that almost all Wikis will automatically store document versions and track changes. This way person who made mistake can always easily be identified and document can easily be rolled back to previous version.  

After you created infrastructure for easy and fast document manipulation you still need to create **firm climate (culture) to motivate people to contribute to knowledge base**. This is the only way that firm knowledge will grow and knowledge will be effectively passed between coworkers. After all, what are [knowledge workers](http://en.wikipedia.org/wiki/Knowledge_worker) without good knowledge base?

In my next post I will write about what should be documented and how, so if you are interested hook up to my [blog feed](http://feeds.feedburner.com/Vukoje) and stay tuned.  
What are your experiences with writing software documentation? 