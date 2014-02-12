---
layout: post
title: "Updated ExtJs4 Mock Ajax Library for Jasmine"
date: 2013-04-02 14:17
comments: true
categories: 
---
[@kenspirit](https://twitter.com/kenspirit) does a nice job in this series ([part 1](http://www.thinkingincrowd.me/blog/2012/08/13/extjs-jasmine-unit-test-part-1-philosophy-and-test-for-store/) and [part 2](http://www.thinkingincrowd.me/blog/2012/08/30/extjs-jasmine-unit-test-part-2-ajax-behavior-2/)) of blog posts talking about some of the pain points (Stores, Ajax handling) of unit testing ExtJS applications.  While [@kenspirit](https://twitter.com/kenspirit) provides a nice adaptation of [jasmine-ajax](https://github.com/pivotal/jasmine-ajax) for ExtJs (as jasmine-ajax only supports JQuery and Prototype currently), that adaptation does not work with ExtJS4.  The following [updated version should work - at least for basic Ajax mocking](https://gist.github.com/zachlendon/5295365).  Let me know if you have issues and I can (futher) update and improve upon this latest adaptation.