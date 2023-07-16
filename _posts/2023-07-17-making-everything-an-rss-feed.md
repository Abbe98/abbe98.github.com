---
layout: post
title: Making Everything an RSS Feed
description: A while back I made a goal along the line of "make all the data on fornpunkt.se available as an RSS feed".
tags:
  - fornpunkt
  - rss
---
A while back I made a goal along the line of "make all the data on [fornpunkt.se](https://byabbe.se/2022/01/08/notes-on-launching-an-mvp) available as an RSS feed". One might ask why, well, I think that one shouldn't be required to use the FornPunkt website to access and reuse its content. I also think that RSS is a great format for this given that most content has a temporal component to it and that RSS has many great clients, integrations, and extensions.

 - All posts? A GeoRSS feed.
 - All posts with a given tag? A GeoRSS feed.
 - All posts by a given user? A GeoRSS feed, optionally with an access token.
 - All tags? An RSS feed.
 - Comments? An RSS feed.
 - All comments on a given post? An RSS feed.
 - All comments by a given user? An RSS feed, optionally with an access token.
 - Comments classified as damage reposts? An RSS feed.
 - Annotations? An RSS feed.

And so on. Some of these are more useful than others. The GeoRSS ones appear to be rather popular while the "Comments on a given post" is not very much used. Ii wasn't much overhead to add these feeds as I already had two [base classes for RSS and GeoRSS feeds in the core Django application](https://docs.djangoproject.com/en/4.2/ref/contrib/syndication/).

In the end not only do users end up with the option to use one of many RSS clients, but there is also an extra set of APIs that might be more accessible than many of the [other APIs](https://fornpunkt.se/data/) given that RSS is a well-known format and that it is easy to discover. Will I keep to this goal? Will I expand it to other sites? I don't know, but given the low overhead in this case I do not yet regret it.
