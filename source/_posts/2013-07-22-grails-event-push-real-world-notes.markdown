---
layout: post
title: "Grails Event Push real-world notes"
date: 2013-07-22 14:32
comments: true
categories: 
---
Today's excellent talk by Colin Harrington at [GR8ConfUS](gr8conf.us) on ASync and in particular the Events Push plugin has me wanting to note some thoughts I've developed through using the plugin at my current client.

First off, I use the following BuildConfig.groovy definition, so that I can exclude the resources plugin version used by the plugin:

        compile("org.grails.plugins:events-push:1.0.M7") {
            excludes 'resources', 'org.atmosphere:atmosphere-runtime'
        }
        
        