---
layout: post
title: "Log4Javascript - Quick Intro and a LocalStorage Custom Appender"
date: 2012-11-12 20:52
comments: true
categories: 
---
With the continuing shift to the client-side for more and more processing in today's web applications, be they mobile-specific or not, effective logging of the running state of the client-side part of your application is critical.  There are a bevy of different solutions to your client-side logging needs, and I present this customization of [Log4Javascript](http://log4javascript.org/) as not an endorsement of [Log4Javascript](http://log4javascript.org/) as any sort of holy grail - but it is inevitably a demonstration that it is a viable, customizable solution that you should consider if you are working on a project that has needs in this area.

[Log4Javascript](http://log4javascript.org/) comes with a collection of appenders and a grouping of logging levels that gives you the type of logging you've probably grown accustomed to in your server-side development efforts.  Hop over to this JSFiddle and look at a sample Hello World type example that would output a log message to your [Browser Console](http://jsfiddle.net/QpK4t/10/)

Beyond having appenders that write to the console, out of the box, [Log4Javascript](http://log4javascript.org/) includes appenders that write to popups, alert, and submit ajax requests to the server.  Using any combination of them are pretty simple operations - they include different options, and can be combined to provide a flexible yet powerful logging strategy.

The proposed LocalStorageAppender I reference adds to this toolkit by providing the ability to store log messages in a browser's LocalStorage, if available. This can be an effective way to store messages for later use, if needed. For example, if you get an error later in the running of your application, wouldn't it be nice to upload a set of log messages that happened before the error on the client side, along with the actual error?  And if you didn't have an error, not to post anything? 

For the proposed LocalStorageAppender, I leverage [Store.js](https://github.com/marcuswestin/store.js), a "stupid simple" micro javascript framework for interacting with LocalStorage.  As with the introductory example earlier, let's first look at the core, working code that logs to LocalStorage in JSFiddle.  To see it working, check out in your browser development tools (Firebug/Chrome Developer Tools/etc) your LocalStorage resource pane to see the "Hello World" log message [jsfiddle.jshell.net logging "Hello World" under a timestamped key](http://jsfiddle.net/QpK4t/12/)

Let's break down the 'running example' code a bit here.

{%gist 4063813 %}

Here we set up our appender object with some pretty self-explanatory functions that all log4javascript appenders need to implement.

The nuts and bolts of our appender is in the append method, so let's look at that

{%gist 4063826 %}

The getFormattedMessage function is the same as the one used for the BrowserConsoleAppender - nothing particularly special for our use case. You'll see that I then use Store.js to see if the browser supports LocalStorage, and if it does I store the message in LocalStorage with a timestamped key.  You could certainly be more fancy with how you determine what your 'keys' are but this assures them to be unique (obviously important) and provides a simple, (hopefully) understandable example.

You'll then see an example use case where one could, if the loggingEvent has a level that meets a certain threshhold (you could also choose to log events that exceed a certain threshhold), one can get all messages, and format them into a string, separated by newlines, with the last log message presented in the beginning of the string, and a "log stack" of messages for all the messages scooped up from LocalStroage. Those messages are then posted to the server, and upon our success handler  the LocalStorage store is cleared.

Additional items to think about when using this type of logging appender includes cleaning up the LocalStorage data you have added when it is no longer useful - for example, upon entry/exit of portions of your application.  

I think using LocalStorage is a nice approach for local through production environment client-side logging as it provides a way to consistenly log the client portion of your application and selectively report back to the server when you have issues.  It especially hits a nice sweet spot for mobile web applications where client-side code execution/handling can unexpectedly vary across OS's and their various browsers.
