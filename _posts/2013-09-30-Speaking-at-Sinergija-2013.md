---
layout: post
title:  Speaking at Sinergija 2013
date:   2013-09-30 12:00:00 +0100
categories: 
---

![SinergijaLogo][1]

I will be speaking at this year's [Sinergija][2].

Presentation is titled _**State of the art logging**_ and here are my incomplete notes for it:

* How to build state of the art production system instrumenting so you can easily understand what is going on in your production system?
* Which component to use? [Log4Net][3], [NLog][4], System.Trace, custom solution…
* Event vs. Trace (Monitoring vs. Performance)
* [Negative events][5]
* Tracing steps with "using" notation (e.g. [MiniProfiler][6])
* [AOP][7] vs. [manual logging][8]
* Where to output data?
* How to scope data?
* How not to kill app performance?
* How to bake in app profiler in your tracing lib?
* Demo of [Webcom][9] powerful GUI for trace analytics system.
* Demo of AOP logging in MVC web app using NLog.

[1]: {{ site.url}}/assets/posts/SinergijaLogo.png "SinergijaLogo"
[2]: http://www.mssinergija.net/sr/sinergija13/konferencija/Pages/Agenda.aspx
[3]: http://logging.apache.org/log4net/
[4]: http://nlog-project.org/
[5]: http://ayende.com/blog/153409/do-you-monitor-negative-events
[6]: http://miniprofiler.com/
[7]: http://ayende.com/blog/3474/logging-the-aop-way
[8]: http://www.udidahan.com/2008/08/01/logging-the-smart-way/
[9]: http://webcominc.com/