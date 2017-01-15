---
layout: post
title:  Integrating responsive site in Salesforce1
date:   2014-11-02 12:00:00 +0100
categories: technology
---

As you probably already know, [Salesforce](http://www.salesforce.com/) (SF) has built their native app [Salesforce1](https://developer.salesforce.com/platform/overview) (SF1) and because SF is such a big hit there is a high chance you app will need to integrate with SF1, which could cause you problems. SF1 is native app which is extendable not by writing native code but by integrating with web apps. Now as native usually means iOS, this integration leads us to dreadful **mobile Safari iframe**.

# The Pain

So here you are, you need to open your app in safari mobile iframe which sucks… and chances are you’ll want to open your existing web app with [responsive design](http://en.wikipedia.org/wiki/Responsive_web_design) that adjusts to mobile screen sizes. Responsive design means general purpose design that adjusts to various screen sizes and as such it is much more complex than pure mobile site. This complexity significantly lowers your chances of working properly in safari mobile iframe.

![]({{ site.url }}/assets/posts/world-of-pain.png)

When I opened my site it was complete agony because it had completely unpredictable behavior. It would reset scroll position in middle of page scrolling and page width would change constantly causing elements to jump around constantly. Occasionally SF1 would crash and wouldn’t open my site again until I reinstalled SF1 app.

I spent few days working on a solution which I wanted to share with everyone and hopefully ease someone’s suffering.

# The Solution

In order to fix problem with flickering and iframe width changing I needed to **set iframe width to exact value in pixels**. Setting width to 100% simply wouldn’t work so I would calculate window width in JavaScript and set it dynamically to iframe.

Now I was left with the problem of scrolling. Unlikely any other browser, mobile Safari iframe expands vertically to display the full document which it contains. There are [various strategies](http://dev.magnolia-cms.com/blog/2012/05/strategies-for-the-iframe-on-the-ipad-problem/) for “implementing” iframe scrolling on mobile Safari. At the end I fixed this by setting **scrolling="no"** and **style="overflow: hidden”** on iframe. I also set iframe height to window size which I calculated same way as window height. I added this height to iframe url as query string which on the other hand I used to **resize my site and actually have scrolling on site instead on iframe**.

Below is the code I have embeded in my SF page.

<script src="https://gist.github.com/vukoje/76a81ba6fdedc202e55e.js"></script>