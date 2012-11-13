---
layout: post
title: "Backbone.js: from Hashbangs to HTML5 PushState"
date: 2012-02-21 22:45
comments: true
categories: 
---
All kinds of [talk lately](http://isolani.co.uk/blog/javascript/BreakingTheWebWithHashBangs) about hash-bang URLs (http://url#fragment) and how they will lead to the end of civilization (seemingly) this coming December.  I was one of the guilty parties, implementing hash-bangs in a heavy AJAX mobile application I've been working on, even though nearly (if not) all of the browsers the users would have would support [HTML5 PushState](http://dev.w3.org/html5/spec-author-view/history.html#dom-history-pushstate).  I did this being aware of the burdgeoning holy war, and had always intended to convert.  It actually fits more cleanly into the conventions of the Grails back-end for the application - i.e., http://url/fragment - and it's HTML5, the future - plus all the other reasons those articles allude to (however opinionated or valid they might actually be).  Nevertheless, my two-staged approach was more a matter of already knowing how to do the hash-bang approach and needing to understand better the pushState approach prior to implementing it.

Much of the mobile webapp in question is built upon [Backbone.js](http://documentcloud.github.com/backbone/)  (which is AWESOME) - and I find it can often take a bit of investigative work (blog/documentation/source code reading + experimentation) to figure out exactly how to do something 'well'.  It's really pretty simple to switch between a 'hashbang' approach and a pushState approach with backbone.js - but it didn't always seem that way.  First some setup then some key takeaways:

Typically at some point in your backbone.js MVC workflow you are updating the state of your models and/or collections on the front-end through communicating with the server.  As a result, backbone.js will fire a corresponding add, remove or reset event, which you as the event-informed developer will hook into and bind your own JS function(s) against.  If you wish to update the browser url - such that it is bookmarkable and works as a state in your browser's history - you'll typically do this here.

So there's your background.  Now let's look at the two scaled down versions of common backbone.js use cases and discuss the subtle different of approach - first hashbang:

{% gist 1881657 %}

then HTML5 pushState:

{% gist 1881650 %}

They look pretty similar.  Note that with the pushState version we have a $.mobile.pushStateEnabled = false;.  That's so if our project has JQuery Mobile that it plays nicely.  There's the whole {pushState:true} option declaration when starting the backbone history, but that's pretty evident/expected.  Notice with the router that the pushState version has the /contextPath before the :toDoId while the hashbang version just has the :toDoId.  Backbone's history functionality has the concept of a 'root' url - where presumably one could set the contextPath and all url's in your backbone implementation would be based off of that, but I found in practice that my url's at best weren't consistent on when they did or didn't use that root definition.  So I'd almost recommend seeing if a root url works for you (especially if you have no contextPath) but having this as your fallback. I almost found it clearer to define the full context path where needed - as opposed to having a root path used in Backbone history - and ensuring it would work there - and then leveraging a context path elsewhere - vs. just being explicit across the few areas where url's exist in one's backbone app.  Nevertheless, I could imagine this 'base root context path' being configured as a global variable (or in general be configurable) for some apps where the contextPath could change based on environment (helping bring consistency to your url syntax across your backbone.js layer), but for my use case I haven't crossed that bridge yet.

Back on topic, note the:

Backbone.history.navigate('#' + this.model.toJSON().id);

vs.

Backbone.history.navigate('/todos/' + this.model.toJSON().id, {trigger: true});

This in general seems pretty sensible, but the trigger scenario is significant here (and is noted in the backbone docs) - so that my loadTodo router method gets called.  With the hashbang approach, the hashchange event was just being picked up and the router method was getting called by backbone.  I believe there's something I could be doing where the router function in question could automatically be called in both scenarios - but it's good to know that if the router method isn't getting called that this option is the cure.  It's much more elegant at least than the manual calls to the router method that you see in some online examples.

Other than that, you're really set.  Regardless of implementation, the "requirement" is that the url's you "save" should be bookmarkable - i.e., not broken at least and should presumably show the same state of the app that the user sees when the url is initially presented.  That makes them also convenient to use as the identifiers in your history, as in the end you are manipulating the browser's 'back' history state, should your user use the browser's back button in your javascript heavy application.   And even though in practice backbone.js is most ideal in SPA (single page architecture) applications, even in those applications, being able to return to previous view states is often a requirement.  One trick in restoring these 'states' is often the models you need to re-render those states are in the backbone collections you already have locally, so you may just be able to grab the right models (based on one or more identifiers in the url) and re-render the view.  There's also the option that you've chosen to cache an HTML5 page in the DOM and can simply transition to that page in your UI upon navigating to particular points in your Backbone.js history.

So while this code hopefully helps provide some examples for the UI prospective, don't forget the back-end piece of ensuring that the url's you are saving can be returned to and provide valid results.



