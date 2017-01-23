---
layout: post
title:  Thoughts on logger lib design
date:   2014-06-14 12:00:00 +0100
categories: principles
---

Last year I gave a talk [State of the art logging](http://vukoje.net/post/2013/10/23/Sinergija-2013-presentation-material.aspx) where I discussed logging, logging libraries and tools for logs analysis. I wanted to go a step back and share with you my notes on designing a logging library. I actually written down what was important for me and later decided to go with custom logger implementation that wraps [NLog](http://nlog-project.org/).

When I talk about logging I always tell a difference between tracing and event logging. By tracing I mean logs with high detail data useful for debugging app. Trace is available only in “tracing mode” – trace data is not collected by default. By event logging I mean data that application outputs to some persistent store and which are used for monitoring application behavior (e.g. crash reports).

# Tracing

Tracing must have **high performance**:

*   It should have no performance impact if not turned on
*   String formatting should not be done if tracing is turned on (Tracing client code never formats string because formatting consumes time and it might not be needed)
*   It should have very small memory consumption when tracing is turned off.
*   When turned on it must not endanger app pool execution (e.g. production tracing must not cause out of memory exception).

Tracing should be enabled **per session** in web applications (multitenant or not) but should also work in cases where session doesn’t exist (tracing win services, tracing web applications before session initialization).

Tracing should support **priority levels** and **labels** (categories).

Tracing should support “Start – End” style logs with **using** **statement**. This will make tracing API better (smaller and more readable code) and make performance monitoring easier (time of method execution). It should also enable hierarchy displaying of trace data (similar to Call stacks in debugging).

If Tracing component uses external components this must be hidden (our trace will wrap them) because otherwise it would introduce high coupling to that external component and make any changes very hard.

Trace should support **logging to file**. File system organization for web multitenant applications should be like this: Root folder/tenant name/user name/date/request time stamp.log Programmer should be able to configure simpler folder structure in simpler cases (Windows service that doesn’t have tenant or user). Root folder should be configurable. If session is not yet initialized or is lost, files should be logged to Root folder/tenant name/.

In web applications it should be possible to trace each web request in **separate trace file**. In other cases programmer should be able to decide when to split file (per day, month, never…).

Trace should have **buffer of last N relevant trace calls** (probably only logs with highest priority). N constant should be possible to configure by programmers. Beside this buffer of last N relevant logs we might keep full trace of last HTTP request. This can be useful when tracing is not turned on and application breaks. In this case we might still want full trace form request that broke the app. This solution might compromise memory so we must be careful with it.

Trace files older by some period should be **deleted in some time intervals**.

**Tracing must not break in production!** Breaking is only ok in debug mode. E.g. if programmer supplies trace with invalid parameters, Trace should break only in debug mode.

# Event logging

Event log should contain information about events in application that are of interest to people monitoring application health and configuration status.

Event log should support **Event log types**:

*   Breaking error
*   Handled error
*   Info
*   Warning

It should be possible to **search and filer event log data**. E.g. show me today’s breaking errors or show me yesterday information containing text “salesforce.com sync started”.

Event logs should contain **enough useful data** for understanding event details. E.g. braking errors should contain following data:

*   User name or logged in user
*   Application name (multiple applications might be logging events to same DB)
*   Exception data (call stack…)
*   Http request data
*   Trace buffer (what did User do before error – useful for extracting reproduction steps)

Events should be **logged to DB and files**. Logging to file is needed for:

*   applications that don’t have DB
*   logging DB access errors (e.g. invalid DB connection string)

**Event logging must not break in production!** Breaking is only ok in debug mode. E.g. if event log DB is not accessible, Event logger should not break.

It would be nice to have feature where **Event Logs can be updated** by support team with comment (e.g. “Known issue”, “Bug 123 created”, ”Resolved”…).

Event logging should **not be transactional**. If Event is being logged in some outer transaction and that transaction is rolled back, the event is still logged.
