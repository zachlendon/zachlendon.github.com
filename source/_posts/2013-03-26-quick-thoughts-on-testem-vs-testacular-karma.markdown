---
layout: post
title: "Thoughts on Testem vs Testacular (Karma)"
date: 2013-03-26 00:25
comments: true
categories: 
---
Both [Testacular](http://karma-runner.github.com/0.8/index.html) - recently renamed 'Karma' and [Testem](https://github.com/airportyh/testem) are great test runners for improving your javascript unit testing workflow.  While Karma was developed as part of AngularJS, it is certainly useful as a test runner for javascript unit tests regardless of frameworks and/or libraries leveraged.  Key features that both Testem and Karma have include:

* Support for running/driving multiple browsers simultaneously, including headless browsers (i.e., PhantomJS)
* Support for the main testing libraries out there - QUnit, Jasmine, Mocha, etc.
* Both will watch the source/test files (that you selectively configure) for changes and automatically re-run tests
* Both provide support for local and CI use
* Both are terminal focused

For me I have found that I have a slight preference for Testem, for a few reasons.  One is the Text User Interface:


{% img  /images/green.png %}

which allows you to better visually see the test results by browsers, whereas Testacular provides this as straight output text lines:

{% img  /images/output.png %} 

Secondly, the ability to also run tests from a browser is a nice alternative when the terminal is not providing you as much flexibility as you want in certain testing scenarios and development workflows.  Configuring this option alongside testem is much more doable than alongside Karma.  The minimal configuration that is required is described in the 'Node Travelers' Toolchain blogpost (in the [icing on the cake section](http://blog.nodetraveller.com/Javascript/My-javascript-testing-toolchain.html)).  As is the case in the terminal, the main benefit over a normal Jasmine/browser TDD workflow is that with this testem integration we get watching of changes and automatic reload of the browser on changes. As a small aside, I've always found the [Jasmine Bootstrap Reporter](https://github.com/esbie/jasmine-bootstrap) to be a great reporter for browser Jasmine reports and significantly better than the default Jasmine Html reporters.  

{% img  /images/jasmineHtml.png %}

 Do note that when using testem with Jasmine that you may have to slightly modify your Jasmine javascript source to ensure that the #testem hashtag is honored when choosing to run a suite of tests or individual tests from the browser.

On the Karma side, I must admit that Karma does seem to have nice debugging integration into Webstorm IDE, an IDE that I've tried but never really used extensively.  I also know Sublime Text 2 has [similar javascript debugging support available of late](http://sokolovstas.github.com/SublimeWebInspector/), so it's possible that Karma's debugging support is stronger than Testem and that leveraging it on an ongoing basis would prove its value.  You'll note in the Karma documentation "video" that support for "dumping" object state, console logging to the terminal, etc. provides a pretty strong workflow from Karma for those who want their javascript development TDD workflow view to look like a Sublime Text editor on one side of the screen and a terminal window on the other.  This editor/terminal workflow is philosophically inline with what Testem is aiming for as well though, so I'm not sure you're really losing this if your workflow fits one IDE/coding/execution paradigm vs. any other.

Ultimately both Karma and Testem will work for your javascript unit testing workflows and they are better than the alternative - no javascript unit tests and/or no javascript unit test runner.  I have found evidence that helps confirm my impression that Testem seems to have been around longer as a project (and thus be a bit more mature), have a bit better documentation, and be more widely used.  I'd also be remiss not to say that I have also found it mildly annoying that Google Search Result links to "Testacular" Google Groups posts are "dead ends", as the group has been renamed (to Karma).  When there is ultimately such a small difference between a set of frameworks and/or libraries, it is to me these little things that can add up and - for now - would make me lean towards and recommend Testem.  That being said, hopefully we'll continue to see innovation from both of these tools and therefore hopefully the story on their usefulness and viability is only in the early stages.