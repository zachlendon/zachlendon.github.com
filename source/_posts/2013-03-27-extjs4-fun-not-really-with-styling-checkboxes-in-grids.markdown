---
layout: post
title: "ExtJS4: Fun (not really) with styling checkboxes in grids"
date: 2013-03-27 23:57
comments: true
categories: 
---
['boxready'](http://www.sencha.com/blog/optimizing-ext-js-4-1-based-applications) is a good event to listen to to change checkbox CSS styles programmatically when using [CheckboxModels](http://docs.sencha.com/ext-js/4-1/#!/api/Ext.selection.CheckboxModel) in an extJS4 panel where the 'grid' is defined as an 'item' in a panel.  When you are defining an actual 'grid' component though (i.e., when you are doing more than simply tying an extJS 'store' to a standard grid component via an item) and want to change checkboxes within a grid listener, you'll want to use the 'viewready' event instead - with a 'defer' to boot.  I admit that it seems that there should be another event that one could use and not have to do a 'defer' timing hack, but so far my attempts at trying other events have proven fruitless (I'd love to be advised differently).  All of these events in question are shown in [AbstractView's source](http://docs.sencha.com/ext-js/4-1/source/AbstractView.html#Ext-view-AbstractView), and when using extJS4+ it's worthwhile to understand all that goes on in this class, especially event-wise. 

The reason one needs to do this styling logic within these events is that the style changes must be applied after everything in your component is visible and any styles are calculated and applied to elements within that component.  While you would think you could do these style settings when you instantiate the CheckboxModel and have them honored, and  there are random illusions to this working online - you will find that it will fail you under certain scenarios.  As an example, 'headerConfig' in CheckboxModel has a headerWidth property.  Howevever, if you look at [CheckboxModel's source](https://code.google.com/p/extjs4/source/browse/trunk/ext4/extjs/src/selection/CheckboxModel.js?r=3), setting the config does not appear to actually change it's value (and in practice this is what I've seen).  In certain grid scenarios, depending especially on the 'flex' property of other columns, you may (ok - will) find ExtJS4+ re-sizing your checkbox columns to excessive sizes - usually on the big end, but potentially too small based on your requirements.

While it is possible and in practice probably better 'code quality' to actually get the grid or panel component (using Ext.getCmp() - by id) and then access the CheckboxModel using a ComponentQuery selector - and then change it's width, another approach is to do it in a more JQuery-like fashion (in Sencha syntax of course).  I quite honestly find this to be a bit easier to do, and when working with Sencha, sometimes easy is really welcomed.  This is also satisfactorily safe to do in my opinion if you don't have lots of elements on a page such that the querying performance of these operations will impact the usability of your app.  With a pretty complex app I've not seen the below queries suffer performance-wise:

{% gist 5260802 %}

The above code would change the checkboxes in the first row of a grid - the first item finding the styled header checkbox (so you can select all rows) and the second loop finding all rows and grabbing the first element from that row.  Yes, you don't need the 'each' necessarily in the first scenario, but it doesn't hurt anything either.

While extJS4 and Sencha Touch continue to prove to be very powerful frameworks, understanding their nuances and pain points continues to be an interesting journey to be embarking upon.


