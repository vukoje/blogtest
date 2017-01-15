---
layout: post
title:  Cross domain RESTful API calls?
date:   2014-10-21 12:00:00 +0100
categories: technology
---

Maybe you started moving more of your web app logic to client and relying on RESTful services for client-server communication knowing that someday other people will be able to reuse these services as remote API to you app. When I did, I knew that there was a problem with calling restful services from other site’s JavaScript because of the [same origin policy](http://en.wikipedia.org/wiki/Same-origin_policy) that forbids browser to make cross domain Ajax calls, but I also knew that all the major web sites allow restful services consuming from JavaScript.

I investigated a bit and here are alternatives I found for this problem.

# JSONP

[JSONP](http://en.wikipedia.org/wiki/JSONP) is browser hack that became standard solution for cross domain Ajax calls. Browser is hacked by pretending that service is static JavaScript file. In order for this hack to work, server must support JSONP, which means you might be required to alter your services a bit.

Main issue with JSONP is that it **doesn’t support HTTP POST** (only HTTP GET). Another potential problem with JSONP is that is **not asynchronous**, which means that it would probably block browser which would lead to poor user experience.

# CORS

[Cross-origin resource sharing (CORS)](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) is new standard that allows cross-domain Ajax calls. Main issue is that [not all main browses are supported](http://caniuse.com/cors). Biggest problem is [partial support in IE8/9](http://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx) of which next limitations are biggest problem:

*   Only text/plain is supported for the request's Content-Type header
*   No authentication or cookies will be sent with the request

# Server Proxy

Another alternative would be to use server proxy that would execute cross-domain request. In other words, do cross-domain request on server instead in browser because server doesn’t have Same-origin policy limitation. The disadvantage is additional work for your clients that must code server proxy instead of consuming your API right from JavaScript.

![]({{ site.url }}/assets/posts/server-proxy.png)

# iFrame integration

Although iFrames have cross domain restrictions like Ajax, they are much more flexible, so hidden iFrame can be used to enable cross-domain Ajax. 3<sup>rd</sup> party web page could load our special iFrame for that could execute Ajax calls in behalf of 3<sup>rd</sup> party page because it is on same domain as our API, and then it can send data back to page. For cross origin iFrame communication [Window.postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window.postMessage) can be used or [easyXDM](http://easyxdm.net/wp/) library if older browsers need to be supported.

![]({{ site.url }}/assets/posts/iframe.png)

# Resources

*   [So, JSONP or CORS? - Stack Overflow](http://stackoverflow.com/questions/12296910/so-jsonp-or-cors)
*   [Enabling JSONP calls on ASP.NET MVC](http://blogorama.nerdworks.in/enablingjsonpcallsonaspnetmvc/)
*   [Cross-domain JsonP using Asp.net MVC and jQuery - Nathan Bridgewater](http://www.integratedwebsystems.com/2010/07/cross-domain-jsonp-using-asp-net-mvc-and-jquery/)
*   [enabling cross-origin resource sharing on IIS7](http://stackoverflow.com/questions/12458444/enabling-cross-origin-resource-sharing-on-iis7)
*   [Facebook and Cross domain messaging clarification?](https://stackoverflow.com/questions/16862207/facebook-and-cross-domain-messaging-clarification)