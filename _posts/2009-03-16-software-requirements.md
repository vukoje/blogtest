---
layout: post
title:  software requirements
date:   2009-03-16 12:00:00 +0100
categories: software documentation
---

![]({{ site.url }}/assets/posts/requirements.jpg)

In my earlier posts I have written about [why should software be documented](/post/2008/12/23/Should-software-be-documented.aspx "why should software be documented") and [what should we document](/post/2009/03/01/What-should-we-document.aspx "what should we document"), and today I will write about software requirements. Requirements are written documents that **describe system** that should be developed and serve as **communication tool** between customers and developers. Requirements are also **thinking tools** that help you understand what you need to build so you don't waste money building the wrong thing.  

"The very act of writing a specification forces you to think through the design you thought you had in your head, and helps you see the flaws in it quickly so that you can iterate and try more designs. Teams that use functional specifications have better designed products, because they had the opportunity to explore more possible solutions quickly. They also write code faster, because they have a clearer picture when they start of what’s going to be needed." [[Joel on Software](http://www.joelonsoftware.com/items/2009/03/09.html "Joel on Software")]

# Approach to writing requirements

You can organize your requirements in more or less formal or agile fashion but the main point in requirements isn't the document templates and complex diagrams. The main point is information. I learned this from few starting chapters of [Writing Effective Use Cases (Alistair Cockburn)](http://www.amazon.com/Writing-Effective-Cases-Software-Development/dp/0201702258/ref=pd_bbs_sr_1?ie=UTF8&s=books&qid=1237119891&sr=8-1 "Writing Effective Use Cases"). I was expecting to find template for Use Cases that will help me write better documentation, and instead I found out that **approach to writing documentation is more important than document template.**

We programmers usually see use cases as boring part of work that is holding back real work and we have urge to begin coding as soon as possible. What happens is **that we don't really analyze requirements, we just write them down and discover errors in requirements when coding** when we already spent solid amount of our time building the wrong thing ("Hmmm, this drop down list shouldn't be here..."). If we took time to think about requirements before implementing them, evaluated hidden problems and scenarios and validated basic business values defined in [project vision](/post/2009/03/01/What-should-we-document.aspx "project vision"), we could detect errors earlier and have more stable requirements which in the end lead to better code and happier programmer life.

# Amount of written requirements

**Having no requirement**s is not a good idea and you can not use agile methodologies as excuse for it. Writing a functional specification is at the very heart of agile development, because it lets you iterate rapidly over many possible designs before you write code. Also r**equirement gold-plating** is another extreme approach that leads to [waterfall software development](http://en.wikipedia.org/wiki/Waterfall_model "aterfall software development") and many of its problems. As always **there is no silver bullet**, you have to find solution that works for you.