---
layout: post
title: Browserconfig.xml in Internet Explorer 11
description: Using browserconfig.xml in Internet Explorer 11 on Windows 8.1.
image: https://byabbe.se/assets/default.png
tags:
  - web technologies
---
Just some days ago a friend wrote to me about a 404 request in Internet Explorer 11 when he was pinning a app to the start screen on Windows 8.1. The app was built with App Ground…

In IE 10 on Windows 8 App Ground did handle pinning using the “msapplication” meta tags. [See this][1].

That was how I dealt with it in App Ground until I looked into this 404 request, When clicking “pin site” in Windows 8.1 the meta tags was used, but at the same time IE sent  a request after `browserconfig.xml`. I search for it and found a [issue][2] over at HTML5boilerplates repo. The browserconfig.xml is a replacement for the meta tags, it’s not backwards compatible… The browserconfig.xml would save bandwidth for the user, because no meta tags is required(if browserconfig.xml is not located in your root you will still need a metatag) and its only loaded when a user actually pins a site. 

For best result you would need four different images, that means four meta tags in IE 10(App Ground was just having one) but still none in IE 11. I decided to drop support for pinned sites in IE 10 and only support IE 11. Now App Ground is using all four images and saves some bandwidth. 

Example use of browserconfig.xml can be seen in [App Ground 1.2.1][3].

All my sources:

 - [IEblog: High Quality Visuals for Pinned Sites in Windows 8][1]
 - [HTML5boilerplate: Add /browserconfig.xml and tile images][2]
 - [MSDN: Creating custom tiles for IE11 websites][4]
 - [Stackoverflow: Windows 8 prepere site for pinning][5]
 - [MSDN: Pinned Sites][6]

PS App Ground is not meant to have great browser support… DS

[1]: http://blogs.msdn.com/b/ie/archive/2012/06/08/high-quality-visuals-for-pinned-sites-in-windows-8.aspx
[2]: https://github.com/h5bp/html5-boilerplate/pull/1481
[3]: https://github.com/Abbe98/App-Ground¨
[4]: http://msdn.microsoft.com/en-us/library/ie/dn455106.aspx
[5]: http://stackoverflow.com/questions/17474389/windows-8-prepare-site-for-pinning
[6]: http://msdn.microsoft.com/en-us/library/ie/hh772707%28v=vs.85%29.aspx
