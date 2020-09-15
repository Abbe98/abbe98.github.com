---
layout: post
title: OMap Mapper a project during the holidays
description: OMap Mapper a project for mapping maps, that I will write during my holidays next week.
tags:
  - omapmapper
---
I got holidays next week and I have some work to do on some projects but I want to do something with maps so during the holidays I will work on a new project...

As you might know I'm an orienteer and I'm in love with maps. I got hundreds of maps, now(and I have a image below to prove it) they are from tons of places most of them here in Sweden but some from other parts of Europe. 
![Some binders with maps][1]

So what I want to do is to visualize all places, on a map, I'm thinking on a heat map or a marker cluster system... Browsing through all my orienteering maps by a map??!! That would be so epic(I like maps...) :-D

**So how will I build this and what techniques will I use?**
I need to improve my PHP so PHP for the back-end, for the database will I use MariaDB because then I use MySQL without using MySQL ;-) I often use a heavy back-end and a light front-end this time I will do the opposite(because of all the map stuff). The PHP part will probably only handle database and user stuff.

The front-end is going to be a bit more advanced...

**My choose of map**
I won't go through why I choosed [Leaflet][2] in this blog post, but I have tested all the major map services and libraries. There is also a great [Marker Cluster plugin][3] for Leaflet that I might use...

**Mustache.js**
Yep a template system, I'm planning to wrap "all" the text content in JSON, so it will be easy to translate it, not because I need it but because it can be useful when I publish it on Github.

The major idea is that I will use PHP to output GeoJSON(P) and JSONP, not totally different from a API-first approach. The map images will not be stored in the database, so exporting will be easier. Hopefully I got a this working by the end of next week :-)

![OMap Mapper techniques][4]

[1]: https://byabbe.se/assets/map-binders.jpg
[2]: http://leafletjs.com
[3]: https://github.com/Leaflet/Leaflet.markercluster
[4]: https://byabbe.se/assets/omapmapper1.png
