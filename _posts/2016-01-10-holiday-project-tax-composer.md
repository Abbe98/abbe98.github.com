---
layout: post
title: Holiday Project Tax Composer
description: My holiday project Tax Composer comes because of a need for creating custom taxonomy schemes for the Biocaching project.
image: https://byabbe.se/assets/tax-composer-scr-1.jpg
tags:
  - biocaching
---
This winter holiday is coming to a close. I have not only been inaccessible in some mountains cross-country skiing all days, although most people seams to believe so. This holiday I actually had two dedicated "holiday projects", a holiday project is simply projects that goes from idea to launched in a single holiday.

Tax Composer comes because of a need for creating custom [taxonomy](https://en.wikipedia.org/wiki/Taxonomy_(biology))(specie hierarchies) schemes for the [Biocaching](http://biocaching.com/) project. Custom schemes allows us to display different taxonomies to for example school classes and bird lovers without touching the scientific one in our database.

Tax Composer is simply a Windows desktop application for building(composing) taxonomy XML schemes from external sources. Currently it supports sources such as the [Encyclopedia of Life](http://eol.org/) and the Norwegian [Artsdatabanken](http://www.artsdatabanken.no/).

### Visual Studio, C\#, & Windows Forms

Last time I wrote C\# I think I was about 10 years old and I was defiantly running Windows XP, when I started this project I thought about Visual Studio as a bloated, overkill piece of expensive software and C# as a not so flexible, documented, open. Also I had "a bit of a issue" with Visual Studio editing my files without me knowing about it.

Now?

Visual Studio and C\# is quite awesome. First of I ditched that expensive Visual Studio Ultimate edition(Enterprise nowadays?) as I had access to. The free Community edition plus a Git(hub) plug in was all I needed. Visual Studio powerful it got awesome debugging features and its auto completing of my code is super useful. C\# is still a static typed language but I has no issues with that, and that behind the scene editing is great.

The only thing I actually have been having a few issues with is Windows Forms, it's great for building basic interfaces fast but it's the "only thing" keeping Tax Composer from being cross platform and isn't responsive. I knew I could use the Windows Presentation Framework instead but it lacks god basic getting started resources(Windows Forms don't even need that) and it would have delayed my actual coding.    

The Tax Composer project was almost the perfect project for getting started with C\# for desktop applications again, it included\:

 - basic input validation
 - saving/editing files
 - HTTP requests
 - XML parsing
 - Custom data types

A few things such as statics and basic graphics could be nice to know too, but this is a good start.

If have found any reason why you would need to build custom taxonomy schemes\:

 - [Download Tax Composer 0.3.0](https://github.com/Biocaching/Tax-Composer/releases/tag/0.3.0)
 - [Browse the source code](https://github.com/Biocaching/Tax-Composer)

![screenshot](https://byabbe.se/assets/tax-composer-scr-1.jpg)
![screenshot](https://byabbe.se/assets/tax-composer-scr-2.png)
