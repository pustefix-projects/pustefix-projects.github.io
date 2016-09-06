---
layout: post
title:  "Finding things"
date:   2013-02-19 16:24:00 +0200
categories: pustefix
---
This blog has been sleeping for almost a year. So it's time to breathe new life into it. Let's start where the last blog entry ended.

Finding things is still an issue. The more complex the application, the greater the need for a simple way to dive into the application, keeping track of where things are located and thus helping you to understand how they interact. Therefor Pustefix 0.18.38 implements a full text search as part of the in-webapp development tooling.

Some developers might argue that they're having their IDE and nerdy command line tools, so there's no need for another search tool. This is almost correct, if you stay within the Java world. But developing a complex view composed of thousands of XML and XSL fragments, located in different modules (available in different forms, like zipped archive or RCS checkout), will require that your IDE is accordingly configured to search all these different locations.

The Pustefix in-webapp full text search is a simple solution to search you webapp without having to use and configure an IDE, e.g. if you just want to test an application without having to set up an IDE project, or if you're an frontend/view developer who wants to stay with the favored text editor. Besides it's useful for debugging, e.g. if resource changes on the file system aren't picked up by the webapp, you can verify from where resources are loaded, etc.

The full text search supports searching the webapp, modules and the classpath based on file name patterns and matching text lines using regular expressions. The search can be found on the pfxinternals page (e.g. local URL: http://localhost:8080/pfxinternals/search).

![Pustefix internals - Full text search](/assets/pfxinternals-search.png)

