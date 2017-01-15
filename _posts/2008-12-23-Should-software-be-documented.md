---
layout: post
title:  Should software be documented?
date:   2008-12-23 12:00:00 +0100
categories: technology
---

First theme I will write about in this blog is software documentation. It feels like natural starting point or at least it should be. Documentation must exist in some shape and volume before you start with development. Documentation purpose is to capture knowledge, keep it from misconception and forgetting. It is important for all participants in software development life cycle, from customer, through PM, developers, tester to users. All of this sounds logical, we have all been taught these things.... so what's the problem?

## The Problem

Problem with documentation is that its creation can be boring and documentation can easily become out of date and useless. Documentation also takes lot of time, which is taken from development.  After all, you can not compile and run your documentation. Because of this, people can easily forget importance of documenting one highly complex system, where misunderstanding is happening on every day basis, and will easily drop it in background when time becomes critical factor... and time is often critical. At the end of the day/deadline, if needed functionalities don't exist, existence of documentation is irrelevant. It is interesting that writing documentation is not problem only to developers urging for freedom and creativity, it is also problem to customer. Customer would usually say that of course he wants his software documented, but at the end of the day he usually won't be willing to participate in its creation, updating and clarification. 

## The Need

Now that I covered some of the problems with documentation there is a question "Why should we bother with writing documentation?”. One of the main attributes of software is **complexity**. Software is usually built to automate some business processes and handle some system complexity transparently. We can say that there are several complexities in software development:

1.  **Domain Complexity** - natural complexity of domain for which software is made.
2.  **Application Complexity** - complexity of application design. This is artificial complexity that can be added for greater reusability, maintainability or can be added by accident.
3.  **Technology Complexity** - complexity of tools and technology used for development.

So we already have three sorts of complexity. That is a lot and only one of those can be pretty large. You should also note that domain can be fairly unknown to customer him self. He could also fail to explain domain to developers, or developers can misunderstand him.

Application complexity can be pretty complex as initial design on paper, with no coding. As system grows, requirements are changing, code is changing, as time runs out developers are hacking their way through code... In worst case, application complexity can reach so high level that no changes are possible and project is dropped.  
As for technology complexity, we all know that technology is changing which doesn't mean it is advancing.

From all above we can conclude two things:

1.  **Software development is hard**.
2.  **Software documentation is very much needed**.

In next post I will be covering some advices on writing documentation so hook up to [blog feed](http://feeds.feedburner.com/Vukoje).