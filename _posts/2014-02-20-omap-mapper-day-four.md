---
layout: post
title: OMap Mapper day four
description: The OMap Mapper project day four, all the database input done and a Leaflet issue.
image: https://byabbe.se/assets/default.png
tags:
  - omapmapper
---
Day four now! 

All the database input is now done, I had the [PDO class][1] since before. I don't deal with sanitizing right now, isn't a application that should run public on the Internet, it's a application that should run on a computer or a file server... I don't know if sanitizing is necessary when the database input is made with PDO prepared statements(need to do my reading). If it's then sanitizing is a part of the Blue Sky...

I did run into a issue with the Marker cluster plugin, when I did remove all the example output and leaved the Feature object empty, Leaflet did not render the map at all so I was not able to select a location or browse the map at all. I do not have a good solution for this, but I have a working, not to bad fix for it. If the database don't have any rows, a GeoJSON example Feature object will be outputted and a example map will be used, if any rows exists this will not be outputted. Doing it this way I both provide a example and fixes the issue.

Then I did all the missing CSS except the forms, but I deal with them fast, and when I did write that it isn't responsive I mean that you need a 1920x1080 screen, not bigger not smaller. :-P

[1]: https://gist.github.com/Abbe98/8862278