---
layout: post
title: OpenStreetMap CLC06 Import Cleanup Part Two
description: My work on cleaning up CLC06 data in OpenStreetMap is done for now.
image: https://byabbe.se/assets/osm-ways-relations.jpg
tags:
  - openstreetmap
---
[In January I proposed](https://byabbe.se/2015/01/05/openstreetmap-clc06-import-cleanup/) cleaning up a lot of imported CLC06 data manually to preserve the OSM ecosystem. Mappers had a hard time working with the large multipolygons and tools such as Tilemill/Mapbox Studio/iD all had rendering issues. Because of those issues the multipolygons become even more broken by mappers trying to handle them.

The two main multipolygons had areas about 80x120KM.

![Overpass image over the multipolygons.](https://byabbe.se/assets/relations.jpg)

### Removed

Today I removed the last major imported multipolygon(the east one). The first one I removed all way back in January, then I spend about a month mapping all the forest back from scratch. I moved on to the next multipolygon and ran into [±5.0 × 10−324 to ±1.7 × 10308](https://msdn.microsoft.com/en-us/library/678hzkk9.aspx) errors and moved on to do [other things](https://byabbe.se/archive.html).

I learned some more powerful Overpass queries and earlier this Sunday morning I pulled the trigger on the second multipolygon, done in less then five minutes. I brutally smashed some "smaller" low quality CLC06 multipolygons into nothing.

Imported CLC06 multipolygons, currently&#58;

![overpass screenshot](https://byabbe.se/assets/osm-relations.jpg)

### Ahead

OpenStreetMap lost tons of data as a result of my work, still I believe that the lose of bad data allow OSM to faster gain high quality data. I mentioned earlier I mapped most of the forest from the first multipolygon back in smaller pieces and with higher quality. Mapping it all back will take time but the forest data will end up being usable.

All the CLC06 relations and ways&#58;

![overpass screenshot](https://byabbe.se/assets/osm-ways-relations.jpg)

As shown in the image above all easy edible such as small not broken multipolygons and areas is still in there, progressive updates of those objects will eventually make the underlying low quality import obsolete.