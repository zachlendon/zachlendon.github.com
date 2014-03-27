---
layout: post
title: "Up and Blogging with Octopress, Mao and GitHub Pages"
date: 2012-02-17 00:34
comments: true
categories: 
---
I've been meaning to get back into blogging for a while.  Blogging seems like the 2006 thing to do, right?  Nevertheless, I really enjoy the technologies I get to work with on an almost daily basis - namely iOS, Grails and various mobile frameworks (JQuery Mobile, Backbone.js, underscore.js, etc.), and hopefully I run across a few things that might be of use to some other people.  At least I'd like to use this blog to help give an outlet to that illusion.  Having a blog also lets me rant about things and have it stored online for an indeterminate amount of time - who doesn't like having their words haunt them for years on end? 

So with all that being said, I've had a long list of weak excuses why I hadn't gotten a blog going, and high on the list was pretty things like 

* Need to figure out where to host it
* Need to figure out what software to use
* Need to figure out what styling to use

Well I've read enough to determine that [Octopress](http://octopress.org) is the developer's [Wordpress](http://wordpress.org) (I probably first noted it being used on Matt Gemmell's blog, and his post [his experiences blogging with Octopress](http://mattgemmell.com/2011/09/12/blogging-with-octopress/)). I also determined [GitHub](http://github.com) is as good of a place as any to host one, for starters at least - and works well with Git-hosted [Octopress](http://octopress.org).  [Octopress's](http://octopress.org) default theme (which this blog uses) provides good enough styling for a developer-centric blog in my opinion - for the time being at least.

For now I'm using [Mouapp](http://mouapp.com) for my Markdown editor - recommended by [@zanthrash](http://zanthrash.com/) - while I thought I liked the idea of [posting to Octopress from MarsEdit](http://danimal.org/blog/2011/07/31/posting-to-octopress-from-marsedit/), I actually like the raw markdown editing better and being able to see the markup in the same window, vs. building html formatted posts.  Plus it isn't that hard to create a new post in Mao, save it to my local blog posts folder, and do a rake generate and deploy - and have it pushed to my github pages repo see it live online - immediately.  I'm sure this will be a process that will scriptable to make it even easier to do with future posts.

A couple things I did note during the process - which probably are obvious to many but weren't initially to me

* To ensure that individual blog pages get generated properly you must have the markdown section rake's new_post command generates at the top of your markdown file
* Strings should be in quotes in your Octopress _config.yml file, or you'll likely get parse errors

If anyone has tips to make the use of these technologies even better going forward please pass them along.
