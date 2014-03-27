---
layout: post
title: "A Sencha Dirty Store Records Quirk"
date: 2013-07-01 10:07
comments: true
categories: 
---
Sencha provides some pretty slick out of the box grid capabilities, one of which, editing, is demonstrated in the ExtJS 4 example [shown here](http://dev.sencha.com/deploy/ext-4.0.1/examples/grid/cell-editing.html).

One example of how Sencha does a great job making the easy hard and the difficult easy (just an opinion I've fashioned over the past several months) is the handling of editing empty cell values.  For one of the apps I work on, I read XML (yes, awesome I know) from a web service data using [Groovy's HTTPBuilder](http://groovy.codehaus.org/modules/http-builder/), which under the covers uses [XmlSlurper](http://groovy.codehaus.org/api/groovy/util/XmlSlurper.html) to parse said data.  When the data is empty, it is by default parsed and represented as "".  When you edit a field in the Sencha grid however, it gets changed to be represented as null.  This therefore marks a record as modified in the Sencha store, when it really hasn't been.  Probably the proper approach to deal with this is to write logic in the Sencha [store update event](http://docs.sencha.com/extjs/4.1.3/#!/api/Ext.data.Store-event-update) to check modified records for this ""/null shenanigans and not allow the update on the modified record to occur.  Once you start making modifications like this for several store objects you'll probably find it best just to get your OOP on and create your own Store object that extends Sencha's with goodies like this.

Ultimately Sencha should in my opinion not mark these records as modified for you.  But it is just another example how Sencha is great at doing heavy lifting but leaves lots of little pieces around for you to deal with - many which you probably shouldn't have to.