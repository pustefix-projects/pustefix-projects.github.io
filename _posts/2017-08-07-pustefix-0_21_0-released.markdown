---
layout: post
title:  "Pustefix 0.21.0 released"
date:   2017-08-07 12:00:00 +0200
categories: pustefix 
---
Pustefix 0.21.0 is available now. The main focus of this release was switching the framework's internal logging from Log4j 1 to SLF4J and adding extended support for the most popular logging backends.

Application developers now can use the logging framework of their choice. It's recommended to use the SLF4J API together with Logback
or Log4j 2 as logging backend. But Log4j 1 is still supported for backwards compatibility.
For details have a look at the [Pustefix reference documentation](/documentation/0.21.x/reference.html#news.0_21_0). 
