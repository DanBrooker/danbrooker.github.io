---
layout: post
title:  "Reactive Cocoa"
date:   2014-10-03 23:23:23
tags:
category: cocoa
published: false
---

Reactive Cocoa is a Functional Reactive Programming paradigm.

This article [If KVO is right, why does it feel so wrong?][kvo-is-right] really sold the need for Reactive Cocoa.

Essentially it wraps observations and notifications and provides you with single interface to it all. It also unobserves automatically.
It can also handles nested key paths, it will automatically observe each component in the path and
unobserve an object when it's no longer in the key path, and the observe the new object. 

##



[kvo-is-right]: https://ianthehenry.com/2014/5/4/kvo-101/
