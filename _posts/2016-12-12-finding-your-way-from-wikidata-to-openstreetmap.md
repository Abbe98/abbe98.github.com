---
layout: post
title: Finding your way from Wikidata to OpenStreetMap
description: I wrote a user script to get you from Wikidata to OpenStreetMap.
image: https://byabbe.se/assets/wikidata-osm-userscript.png
tags:
  - wikimedia
  - openstreetmap
  - maps
redirect_from:
  - /blog/2016/12/12/finding-your-way-from-wikidata-to-openstreetmap
---
Recently there has been multiply discussions about the connections between Wikidata and OpenStreetMap. Many Wikimedians has been concerned about the one way connection through the `wikidata` tag over at OpenStreetMap and the lack of a way to find the corresponding OpenStreetMap element from within Wikidata.

The easiest way in the past has been to head over to [Overpass Turbo](http://overpass-turbo.eu/) and query for the Wikidata id. I would say that even for OSM folks and SparQL hippies it's a bit  of an annoying process. 

Because of this I created a Wikidata UserScript a while ago witch adds a link to the OpenStreetMap Element which has the Wikidata id referenced. 

![screenshot](https://byabbe.se/assets/wikidata-osm-userscript.png)

You can try it out by adding the following line to your `common.js` file\:

```
importScript('User:Abbe98/osm.js');
```

Behind the scene it's using the Overpass API for looking up the OSM element, it's source is available over at [Github](https://github.com/Abbe98/wikidata-osm-link). 
