---
layout: post
title:  About data caching
date:   2012-09-09 12:00:00 +0100
categories: algorithms
---

In my [Code Project](http://www.codeproject.com) article “[Demystifying concurrent lazy load pattern](http://www.codeproject.com/Articles/418425/Demystifying-concurrent-lazy-load-pattern)” I have explained what common mistakes in lazy load implementations and how to implement fast concurrent lazy load cache. In this post I will discuss why caching itself is important and what are some implementation strategies for caching.

![]({{ site.url }}/assets/posts/caching.png)

# Why caching?

Simply put... performance! Usual business application relies on lots of data, and that data usually resides in a database. Because data is out of the application thread, accessing it can be much slower. If external data is on a hard drive (and it usually is), accessing it can be thousands of times slower than accessing data in application memory. The great thing about cached data is that not only it will be few thousand times faster, but it will also scale much better under heavy load than your poor database.

Nowadays, cached data is becoming more and more important with the emergence of high load web sites with many concurrent users. In addition, we see the rise of distributed key-value databases acting as a shared cache.

In our application, we have increased the speed of a critical business feature, Order lines import, for about 50 times after data caching. Speed went from 1 row per second to 50 rows per second.

Sounds great, and best of all it is easy and it just takes a little caring about your data. Unfortunately, I have seen many problematic implementations of caching that will either occasionally break in production or have very low performance and those implementations are the main reason for writing this article.

# Caching strategies

There are several choices to make when implementing a data cache. Some of the facts that could affect these decisions are:

*   The size of the data.
*   How and how often is the data used?
*   How and how often is the data changed?
*   Can eventual consistency (stale data) be tolerated?
*   …

I will give my favorite example. Content Management System (CMS) sites are usually completely dynamic, which means that site menus and page content are created from some model usually defined in a database. This data is rarely changed and it is accessed very often. Imagine this site has a thousand of concurrent users and a busy administrator adding new pages every day. This might seem like data is changed often, but in fact data will be accessed millions of times before it is changed. Once in a day might not seem rare, but measured in processor ticks, it is millions of years. Also, this data is very small which means caching it will not be a big impact to server memory and if some user does not see new pages for a few minutes it is not that big deal.

## Data loading

In [my lazy load pattern article](http://www.codeproject.com/Articles/418425/Demystifying-concurrent-lazy-load-pattern), I was loading all Products at once when building a cache. An alternative to this approach is to load single Product once it is requested, if it is not already loaded in cache. Choosing the right implementation depends on the size of the cached data and its usage pattern.

As I mentioned earlier, Order lines import is a critical process in our application. In this process, we are accessing Supplier data for each Order line that is being imported and there can be few thousand lines being imported. This means we will be accessing the Supplier DB table a few thousand times per process. On the other hand, the Supplier table in DB is quite big and loading it into memory would take too much time and memory. It turns out that in practice, for one importing process (and all lines being imported in it) only a few Suppliers are needed, so a single Supplier caching improved our performance significantly with just 10 lines of code.

## Data accessing

Once you load data in cache, how do you access it? Here are some of the alternatives:

*   **Sequentially** - by iterating through the whole list of Products and looking for matching Product
*   **Directly** - by building some kind of memory index. For example, once we have loaded Products we could have built a hash list in which key is Product Name and value is pointer to Product instance with that name. This would allow us direct access to the Product instance by using its name.
*   **Combined** - by splitting our Product list into smaller lists by some criteria. For example, we access the list of Products with some Product Type directly using a memory index and then iterate over it. Combined access is great choice when you have various criteria for data searching and direct access cannot be applied or preparing all memory indexes would be to time or memory consuming.

When choosing your data access approach you have to weigh the performance vs. complexity increase. Here is an example of a performance gain we got after refactoring our Price Calculator cache:

*   Sequential access - 47ms
*   Combined - 0.02ms

Sometimes it is important for some application logic to work with the data from one point in time because otherwise inconsistent data might appear in the application. If this is the case, logic executing over cached data must be aware that the cache might reload at any time. 

For example, we have a rule that our database contains product A or product B, one of them must exist in the database. Let us say that at time t0 DB contains only product B, and at time t1 a transaction occurs in DB that adds product A and removes product B. 

Below is the code demonstrating the potential problem in this case. 

<center><i>Code sample 1: Inconsistent data cache</i></center>

{% highlight C# %}
// t0: Product A doesn’t exist
If (!this.HasA(Cache.GetProducts()))
{
    // t1: cache is reset (A added, B removed)
    // Product B doesn’t exist so else branch is executed        
    If (this.HasB(Cache.GetProducts()))
    {
        this.UseB(Cache.GetProducts());
    }
    else
    {
        // we reach this part of code which means that
        // DB doesn’t contain product A nor B
        // and this case is not possible
    }
}
{% endhighlight %}

The solution is again simple. We store cache in a local variable to make sure we work with data from one point in time, when this is important.

<center><i>Code sample 2: Consistent data cache</i></center>

{% highlight C# %}
// t0: Product A doesn’t exist 
List<Product> localProduts = Cache.GetProducts();
If (!this.HasA(localProduts))
{
    // t1: cache is reset (A added, B removed)
    // but it doesn’t affect our local variable
    if (this.HasB(localProduts))
    {
        this.UseB(localProduts);
    }
}
{% endhighlight %}

## Cache scope

It is important to understand who is sharing cached data because this fact influences the cache implementation. The goal is also to narrow down the scope as much as possible to gain naturally partitioned data that will have a lower data load and less concurrent reads.

Here are the cache scopes I could think of:

*   **Multiple applications** - Most complex scenario where data is shared by users of multiple applications. Consider using third party solutions for distributed key value stores to handle complexity of distributed cache. Consider having separate cache for each application to avoid the complexity of a distributed cache. Potential problem of this approach could be inconsistent data across applications or too big data load.
*   **Single application** - Data is shared by users of a single application
*   **Database** - If you have single application that connects to different databases when a user logs in, then you should probably cache data per database instance and not per application instance.
*   **Session** - Usually implies user specific data. Nice thing about this cache is that if you store it in application session store, it will naturally expire once the session expires (user logs out or is inactive for some time)
*   **Use case** - in this case, cache is usually reset once form is closed

## Resetting cache

### How?

Usually we can reset cache by reloading data or setting it to null and letting it lazy load of first data request.

In our examples, we have implemented cache resetting by setting cached Product list to null. 

There are few reasons why I do not recommending reloading cache data on cache resetting:

1.  It is slower
2.  Loading logic is duplicated
3.  It is a waste of resources. Instead of loading data as needed, we are always loading it.

### When?

The easiest caching scenario is the one where only the application implementing the cache alters the cached data in DB. In this case, the cache should be reset once data is changed by the application.

If the data is changed by some other application, then caching becomes trickier. You can consider caching data for some time interval if you can tolerate inconsistent data in between. For example, can we tolerate that our product list is refreshed every 30 minutes and can contain stale data?

In our application, we have a service synchronizing our database with external data sources once or few times a day. Once this service is done with synchronization, it triggers a web service to notify the application that synchronization is done. We use this notification to reset our cached data that might have been updated by service.

There were several attempts in .NET to have a cache that will reset automatically once some table in MS SQL Server changes. We tried this approach few years ago and it caused us many headaches. 

# Conclusion

Caching is something you will probably need in your applications, although caching is not perfect and has its downsides. One of the downsides is increased application complexity. You should always weigh complexity gains versus performance gains and add caching only if it significantly increases your performance or scalability.

Do not underestimate power of a DB querying engine and DB indexes and use that as an excuse for caching everything. If your DB data access is slow maybe you should double check DB indexes. If you are sure you need the full edition of Oracle to have good DB performance, check indexes again. Bear in mind that you do not want to end up building your own in memory querying language because you will fail. DBs are better options than cache for large data and for complex data matching criteria.

In our application, we have around ~500.000 Products in the DB, and guess what? We are not caching them because cache building would take too much time and memory. In addition, we have some advanced Product search queries in T-SQL we did not want to code in C#. By the way, once we “optimized” our critical Product search DB queries we got average executions of 1s. Once we dug into the indexes and really optimized queries, we got average 0,01s execution.
