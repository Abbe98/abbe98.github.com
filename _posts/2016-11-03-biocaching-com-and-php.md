---
layout: post
title: Biocaching.com and PHP
description: The main Biocaching client biocaching.com is built with PHP and I was the one responsible for the decision to do it that way.
image: https://byabbe.se/assets/bc-profile-screenshot.png
redirect_from:
  - /blog/2016/11/03/biocaching-com-and-php
---
The main Biocaching client [biocaching.com](https://biocaching.com/) is built with PHP and I was the one responsible for the decision to do it that way.

Although the Biocaching Platform is API first, biocaching.com is not all client side JavaScript. Development speed, easy accessibility, rendering speed and maintainability was all reasons to ditch the idea. 

I considered both Go, Ruby and Node. Node had the advantage of being non-blocking by default. Rails had the advantage of development speed and of being Ruby(Ruby is used all over Biocaching). Go is just not there yet, wasn't there a new package loading solution the other day?

PHP had the advantage of development speed and the fact that's literary made for HTML rendering. No framework needed, the best documentation around and it's easy for anyone to maintain.

Just yesterday I was trying to get the TTFB(time to first byte) decreased on profile pages over at biocaching.com, usually the TTFB is not a issue in most applications but the biocaching.com server application is an API first application making actual HTTP request to the Biocaching API\.\.\.

If you are now thinking how stupid it is to use a blocking language such as PHP for such an application you should do a few Google searches and end up on Stack Overflow a few times.

Aka general development work-flow.

So the reason for the issue on biocaching.com was my logic for rendering all the follow buttons(there can be a lot of them).

![screenshot](https://byabbe.se/assets/bc-profile-screenshot.png)

I started of with my calculator as usually when working on performance issues, did some analytics and decided on a solution that could reduce the TTFB up to 37%! 

Let's just say that my calculation sucked, I was at one point able to measure a improvement at 87%. It's milliseconds but still magic.

If you would like to see more posts about the Biocaching Platform, the sometimes crazy technical solutions and the usage of some of the coolest open datasets around let me know!
