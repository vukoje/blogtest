---
layout: post
title:  Batched by default
date:   2014-01-24 12:00:00 +0100
categories: random thoughts
---

Few weeks ago I was listening to a lecturer explaining how Salesforce works from programmer perspective. Among other things I have noted that SalesForce cares very much about their performance. They care so much that they have forbidden sequential access to the database. This is also why database access API are all designed to work with batches.

Few day ago I was writing MS SQL triggers for the first time after long time. Again I have noted that API for triggers is batched meaning that trigger is called only once after all rows in SQL statement are inserted/updated/deleted. Once trigger is called programmer can access virtual tables containing all altered rows. Off course alternative approach (not batched) would be to call trigger after each row update and this would lead to much poor performance.

Today I have analyzed some slow peace of code that is slow because it is sequentially loading many complex objects from database. At first there was a need to load only single complex object and that is what programmers implemented without support for batching (loading multiple objects at once). Once there was a need to load more objects programmers again did simplest thing - they just run single loader in a loop. Both choices sound logical to me but they lead to some slow peace of code that won’t be optimized without significant effort.

**This lead me to thought that all APIs should be batched by default**. This will lead to faster code and just slightly less convenient API in cases where we work with one object.

# Update:

My friend Andrija Cacanović reminded me that JQuery’s fluent API is nice example of batched API.