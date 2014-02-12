---
layout: post
title: "Using Tincr with Grails for Live Client-Side Reloading"
date: 2012-11-16 23:32
comments: true
categories: 
---
There's various solutions out there for seeing client-side changes quickly in a browser.  One such solution, [livereload.com](http://livereload.com/), was mentioned by Ted Naleid in [this tweet](https://twitter.com/tednaleid/status/269105419274813440).  While I don't have much experience with livereload, I'm not completely convinced I'm doing it wrong (as he suggests somewhat tongue-in-cheek) either (though it wouldn't be the first time I've been wrong).  I have been using another solution, and I wanted to share with you how to start using it with your own Grails application, if you so choose.  The solution I have been leveraging for live-reload-"like" functionality is the Chrome extension [Tincr](http://tin.cr/).  This post attempts to give you a quick guide to leveraging Tincr with your Grails 2.x application and talk briefly about how it helps you iterate your client-side development efforts quicker.

Once you install the Chrome extension, it will show up as a tab in your Chrome Developer Tools view. ![your Chrome Developer tools, like so:](http://s8.postimage.org/5eas13ujn/Screen_Shot_2012_11_16_at_11_38_02_PM.png)

You'll notice that I choose the Configuration File Option in Tincr: 

!['Configuration File option'](http://s13.postimage.org/oop700vtv/Screen_Shot_2012_11_16_at_11_41_23_PM.jpg?noCache=1353130755). 

This allows me to customize the mapping, ideally through regular expressions, between the project's resource files and where they are located in my project.  I do this mapping because I have had issues with it working simply with an http web server, though others might have better success with one of the other pre-configured options. 

Nevertheless, here's an example tincr.json file, which you need to put right under the web-app folder of your project.

{%gist 4093607 %}

As you can see, this basic JSON simply maps js and css resources under the web-app folder, which I set as the Tincr ROOT folder in Chrome, to the project's js/ and cs/ folders.  It works recursively for those directories as well.  You can of course get more fancy depending on how your project's resources are defined.

One 'gotcha' to watch out for is resource bundling.  To get this to work (at least without major pains), I turn resource bundling off in the Grails 2.x apps I use Tincr in by adding:

grails.resources.debug=true

in the development environment config section of my project's Config.groovy file.  While this adds additional parameters to my resource files, it breaks them out of Grails' default bundling strategy and more easily allows Tincr to do its magic.

As for that magic, Tincr allows me to make changes to javascript or CSS files in the browser (in Chrome Developer Tools), use Cmd+S (save shortcut, this being the Mac version of a save shortcut), and have the changes be saved back to the file system (and viewable instantly in my IDE).  On the reverse side, as you can see in the [Tincr documentation](http://tin.cr/docs.html), you can define a 'fromFile' JSON attribute, which will allow you to save a file in your favorite IDE and have Chrome bring in the changes *without* reloading the page in the browser.  Luckily, in this simple configuration example, Tincr is smart enough to reverse-engineer the 'fromFile' mapping, so defining it is redundant, and I have therefore not done so.

So hopefully this provides you an impetus and a guide to start to "tinkering" (you knew it was coming…) with   [Tincr](http://tin.cr/) in your Grails application!