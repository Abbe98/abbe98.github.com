---
layout: post
title: Mapping the Past with OpenHistoricalMap and JOSM
description: Configure JOSM for OpenHistoricalMap and use its powerful tools to improve your mapping.
image: https://i1190.photobucket.com/albums/z458/abbe98/OHM5_zpsu9qezcya.jpg
tags:
  - openhistoricalmap
---

JOSM gives you the power to do OpenHistoricalMap mapping offline, use custom filters, use custom base maps without tools like Map Warper and much more.

First we want to set JOSM to read and write data from OpenHistoricalMap not OpenStreetMap, make sure that JOSM points to `http://www.openhistoricalmap.org/api/` and that you have been updated your username/password:

![Screenshot](https://i1190.photobucket.com/albums/z458/abbe98/OHM1_zpsrody1pzr.jpg)

Too add a custom old map(JPG/PNG/whatever supported) as a layer we will need the plugin PicLayer. Add it by selecting it in the plugin list and click download:

![Screenshot](https://i1190.photobucket.com/albums/z458/abbe98/OHM2_zpswjg6uob1.jpg)

Now we can go ahead and download existing OpenHistoricalMap data, just as we would do from OpenStreetMap:

![Screenshot](https://i1190.photobucket.com/albums/z458/abbe98/OHM3_zpsocsptbdf.jpg)

JOSM might show you a error if no data existed in the selected area if so is the case just ignore it.

Now we can load our base map, select "New background layer from file." and select your file:

![Screenshot](https://i1190.photobucket.com/albums/z458/abbe98/OHM4_zpssyocztw9.jpg)

Now we need to georeference the map layer, do this by selecting it in the layer list and enable it. This will enable tons of tools for scaling and panning your layer. Note that it's totally legal to use Mapbox Satellite for georeferencing your layer, but a GPX track will work just as well.

![Screenshot](https://i1190.photobucket.com/albums/z458/abbe98/OHM5_zpsu9qezcya.jpg)

Just by knowing the PicLayer tools: move, scale and rotate and the native layer opacity feature you will get far. When you have been georeferencing the map go ahead and enable the Datalayer 1 again then left click your custom map layer in the list and save its georeferencing for the future.

Now go ahead and map all the stuff from your base map! Tags such as `source`/`ohm:year` can be added to all objects at once later on. If you don't know the `start_date`/`end_date` for a object, leave it and just provide the `ohm:year` later on.

### Using Filters

If you are working in an area objects from different time periods you will find use for this and other filters `"ohm:year"="1928"`.


When you are done mapping all stuff go ahead and select all objects(not individual nodes) and then add a `source`/`ohm:year` tag, to all objects:

![Screenshot](https://i1190.photobucket.com/albums/z458/abbe98/OHM6_zpsngqr3bqk.jpg)

Done? Just upload it when you are connected to the Internet!