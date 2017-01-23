---
layout: post
title:  Naming is the design
date:   2014-08-10 12:00:00 +0100
categories: principles
---

> There are only two hard things in Computer Science: cache invalidation and **naming things**. - Phil Karlton

Yes, naming is hard but it is also very important. We tend to think that big complex architecture is the software design and that type and member naming along the way is just something that is hard and that we screw up. My point here is that naming is the software design and that on daily basis to me it is more important than architecture.

If naming is good:

*   it will be easier to understand the code and get the big picture
*   API will be simpler to user and there will be less bugs
*   there will be a greater chance that code for some new feature goes to the right place and that software will evolve gracefully instead of becoming a [big ball of mud](http://en.wikipedia.org/wiki/Big_ball_of_mud)

In book [Domain Driven Design](http://www.amazon.com/gp/product/0321125215?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321125215), Eric Evans describes the term **Ubiquitous language** for the practice of building up a common, rigorous language between developer and users, and we can think of this as naming on steroids. Also [Obfuscation](http://en.wikipedia.org/wiki/Obfuscation_(software)) can demonstrate the importance of naming because obfuscated code has worst possible names so that is almost not human readable.

## Naming and Cohesion

> As applied to object-oriented programming, if the methods that serve the given class tend to be similar in many aspects, then the class is said to have high cohesion. In a highly cohesive system, code readability and the likelihood of reuse is increased, while complexity is kept manageable. - [Cohesion](http://en.wikipedia.org/wiki/Cohesion_(computer_science))

IMO **types that have high cohesion are easy to name**. Low cohesion types are hard for naming because usually they are schizophrenic and do many (unrelated things). So we can think of a good name as a necessity that will force good design decisions. 

## Code example

I want to give an example of bad naming that irritated me enough to write this post. Here are some JavaScript DOM Event methods.

*   [cancelable](https://developer.mozilla.org/en-US/docs/Web/API/event.cancelable) - Returns whether or not an event can have its default action prevented
*   [preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/event.preventDefault) - To cancel the event if it is cancelable, meaning that any default action normally taken by the implementation as a result of the event will not occur
*   [defaultPrevented](https://developer.mozilla.org/en-US/docs/Web/API/event.defaultPrevented) - Returns a boolean indicating whether or not event.preventDefault() was called on the event.
*   [bubbles](https://developer.mozilla.org/en-US/docs/Web/API/event.bubbles) - Returns whether or not an event is a bubbling event
*   [stopPropagation()](https://developer.mozilla.org/en-US/docs/Web/API/event.stopPropagation) - To prevent further propagation of an event during event flow
*   [cancelBubble](https://developer.mozilla.org/en-US/docs/Web/API/event.cancelBubble) - Indicates if event bubbling for this event has been canceled or not.

For me it is hard to remember names of function and properties because they are not consistent. Here are some terms that are used interchangeable in API but mean the same thing:

*   stop, cancel, prevent
*   bubble, propagation
*   cancelable, hasDefault

Below is my proposal for renaming this API that should be trivial to remember.


| Old               | New               |
|-------------------|-------------------|
| cancelable        | hasDefault        |
| preventDefault()  | cancelDefault()   |
| defaultPrevented  | isDefaultCanceled |
| bubbles           | bubbles           |
| stopPropagation() | cancelBubling()   |
| cancelBubble      | isBublingCanceled |