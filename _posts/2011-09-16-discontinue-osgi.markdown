---
layout: post
title:  "Pustefix discontinues OSGi work"
date:   2011-09-16 11:50:00 +0200
categories: pustefix
---
More than 2 years ago we started to add OSGi-support to Pustefix. In September 2009 we officially released Pustefix 1.0.0, see an excerpt of the annonuncement:

> Pustefix 1.0.0 has been released. This groundbreaking new release offers full OSGi support, i.e. Pustefix not just can be run inside an OSGi runtime, but Pustefix itself is built on the principles of OSGi, empowering you to modularize all aspects of a webapplication (business logic, view components, etc.) using an OSGi service based extension point mechanism.

Today we officially postpone OSGi support. Actually development stood still for more than a year because of the lack of adoption by our user community. To be honest we have to state that our OSGi experiment has failed and there are evident reasons.

I still think OSGi is a great technology and I'm sure there are a lot of use cases where OSGi already works very well, but the web application development scenarios targeted by Pustefix do not fit (yet).

In a way OSGi offers much more than we need, and at the same time not enough to make it worth paying the price for the effort of introducing a new programming model, a more complex development process and managing the various pitfalls when developing within an environment which itself is not yet ready for OSGi (infrastructure, tools, third party libraries, etc.).

But postponed is not abandoned and we're looking forward to the modularization support coming with JDK 8, Project Jigsaw and JSR 294.

Starting from today the Pustefix main development will take place in the SVN trunk again. The OSGi implementation was moved to a branch and will be further available for backreference.
