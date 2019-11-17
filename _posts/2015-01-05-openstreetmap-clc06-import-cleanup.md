---
layout: post
title: OpenStreetMap CLC06 Import Cleanup
description: The CLC06 import made in 2006 hurts the OSM ecosystem.
image: https://byabbe.se/assets/ways-relations.jpg
tags:
  - openstreetmap
---
When I first got involved in OpenStreetMap all my mapping was done in the iD editor, a great user experience for new users easy to work with and tagging made easy. My first experience with iD and OSM was terrible. It was because of a old low quality forest import that covers a huge area, shown below.

![OSM screenshot][0] 

Most of the import is two massive multipolygons with tons of relations. In iD it was impossible to merge other areas into the multipolygons and the forests had to be heavily remapped. The result of other mappers ways to deal deal with this has lead to two massive multipolygons with broken relations, resulting in rendering issues. First image below shows the quality of the import, the second shows a rendering issue in iD as a result of broken relations(Not related to the [reverse inner bug][2]).

![JSOM screenshot.][2]

![rendering issue in iD.][3]

Below is two screenshots from Overpass Turbo, showing how the imported data looks like in the OSM database. The first image shows both ways and relations, the second just shows relations(multipolygons).

![Ways and relations.][4]

![Relations][5]

The imported multipolygons has become a issue to the OSM ecosystem. It makes it hard for developers and designers to use the data because applications such as Tilemill and Mapbox Studio having rendering issues with the data. It becomes a issue for new mappers that has to remap major areas(in iD this means dragging nodes), that can't merge smaller areas such as lakes and has to deal with relations. 

I'm looking into solutions for splitting the two major multipolygons into pieces along major roads(they should be it anyway) or in a worst case scenario delete them. If anyone has a idea about how we should deal with this please share your knowledge. 

There is other imports like this one in Sweden some of them also from [EEA Corine Land Cover 06][6](Link to latest version of the dataset) but I haven't looked into them as much. I think that we need forest imports at least here but we need to be able to work with them from or usual tools such as JSOM and iD.

Any thoughts?

[Link to related changesets][7]

[0]: https://byabbe.se/assets/base-osm.jpg
[1]: https://github.com/openstreetmap/iD/issues/2259
[2]: https://byabbe.se/assets/jsom.jpg
[3]: https://byabbe.se/assets/broken-id.jpg
[4]: https://byabbe.se/assets/ways-relations.jpg
[5]: https://byabbe.se/assets/relations.jpg
[6]: http://www.eea.europa.eu/data-and-maps/data/corine-land-cover-2006-raster-3
[7]: http://www.openstreetmap.org/user/Sten%20Åkerblom/history#map=9/59.2757/16.4822