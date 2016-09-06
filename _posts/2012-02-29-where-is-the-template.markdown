---
layout: post
title:  "Where the deuce is this template?"
date:   2012-02-29 13:54:00 +0200
categories: pustefix
---
Having highly modularized applications together with Pustefix's multi-level XSL transformations sometimes can be a little bit annoying, e.g. if you want to reproduce a view bug and you don't have a clue how the HTML output is produced and where the involved XSL templates come from.

Therefor Pustefix (since 0.18.10) can visualize the so-called target dependency model, showing you how the XSL stylesheets on each transformation level are composed, which XSL transforms which XML, what XML parts and images are included, etc.

Besides showing the dependency model Pustefix also lists the XSL templates available on the selected transformation level. All XML/XSL files can be directly viewed/downloaded (even if coming from a module archive).

This view is generated as part of the pfxinternals page (e.g. locally accessible in development mode under http://localhost:8080/pfxinternals/targets).

![Pustefix internals - Targets 1](/assets/pfxinternals-targets1.png)
![Pustefix interanls - Targets 2](/assets/pfxinternals-targets2.png)
