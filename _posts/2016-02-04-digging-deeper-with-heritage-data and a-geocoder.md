---
layout: post
title: Digging Deeper with Heritage Data and a Geocoder
description: This article describes a reverse geocoding experiment preformed on heritage data. I'm using reverse geocoding to be able to improve location based search.
image: https://byabbe.se/assets/soch-logo.jpg
tags:
  - soch
---

This article describes a reverse geocoding experiment preformed on Swedish heritage data provided by the SOCH API. I'm using reverse geocoding and a bit of magic to be able to improve location based search by being able to return items that isn't georefrenced. This practice can be applied on almost any dataset.  

**A friend of mine pointed out** that this could be achieved by selecting location names using a usual bounding box. The reason I decided to go with reverse geocoding(expect the fact that's more fun) is that it's more flexible, you can use it along a path or just with a single point without building some rubbish estimated bounding box.

SOCH contains about 1.6 million georefrenced object all accessible from a map, but if you are doing research on a location you will need more then just the georefrenced objects. You will probably end up making a few searches(both free text and location text) on multiply place names in addition to your bounding box search.

All those searches can be automated from the bounding box search.

For my setup I'm using the open source geocoder [Pelias](https://github.com/pelias), with place name data from [OpenStreetMap](http://www.openstreetmap.org/)([pipeline](https://github.com/pelias/openstreetmap)) and [Geonames](http://www.geonames.org/)([pipeline](https://github.com/pelias/geonames))(adding your own data is not a major task either([pelias-model](https://github.com/pelias/model))).

You can use any geocoder with useful data(such as Googles or Mapzens public APIs) but the results will differ.

I will make I urban and one non urban search, the non urban search will happen around Flodafors in S&ouml;rmland Sweden([59.067,16.359](http://www.openstreetmap.org/#map=17/59.06703/16.35998)) near the known church [Floda kyrka](https://sv.wikipedia.org/wiki/Floda_kyrka,_Södermanland), the urban search will happen around the street Vallgatan in Nyk&ouml;ping Sweden([58.74,17.01](http://www.openstreetmap.org/#map=19/58.74887/17.01014)) next to the former castle [Nyk&ouml;pingshus](https://en.wikipedia.org/wiki/Nyköping_Castle).

I have set the geocoder to always give me the ten closest place names, those will then be used in the actual text based searches.

The non urban text based searches resulted in a total of **1724 unique results**, the free-text searches resulted in 1330 results, the text location ones 808 results. 214 results was retrieved both from the free-text searches and the text-location ones.

Only about 40% of the unique results was relevant for the requested location, I expected the useful results to be even fewer so even if 40% seams like a bad result it's actually a good one. It's quite easy to sort out a lot of irrelevant result by searching the objects content for other regions names. If one object contains the name of any region other then the one where the location is located it can be removed from the final results.

The bounding box for a area covering all the places with the used names returned **32 results**.

![statics](https://byabbe.se/assets/reverse-non-urban.png)
![statics](https://byabbe.se/assets/reverse-non-urban-2.png)

The urban area did cause some trouble, as about half of the place names used ended p being useless store names. One of the used place names was the name of the local museum, S&ouml;rmlands Museum even more sadly this did not cause any bad results because this is one museum witch has its collections content behind pay-walls and not available through the SOCH API.

There where **1640 results** unique this time, almost 100 results less then for the non-urban example, this is because store names and boring museums do not provide any results. The text-location searches returned 256 results, only about 20% was useful in this case, mostly because of the fuzzy search behind SOCH(one of the stores contained the name of a church in some foreign area). The free-text searches returned 1384 object in witch about 80% was useful! I came to the conclusion that this was because the name of the former castle Nyk&ouml;pingshus provided many results and did not share the name with any other location(witch was a issue in the non-urban location). 

The relevant bounding box for the urban area returned **13 results**.

![statics](https://byabbe.se/assets/reverse-urban.png)
![statics](https://byabbe.se/assets/reverse-urban-2.png)

It should be noted that the difference in results between the non-urban and the urban area is affected by the fact that the area covered is much larger for the non-urban area as a result of the density of place names.

Although using a reverse geocoder often gave more irrelevant results then relevant ones this is definitely a improved way for searching, manual searches would always give the same irrelevance and much of the irrelevant objects can be sorted out with simple techniques. Using this and a few other tricks has really help me when I have been looking of content deep into the oceans of data. 

I should also note that each location query ended up with eleven HTTP requests to the Kringla.nu MediaRSS interface(cheaty way of using the SOCH API), but if such a search feature would be added into the actual API it would not be super heavy(at least not for you the client).

I'm heading to Helsinki tomorrow for Hack4FI - hack your heritage, as a part of Wikimedia Finlands Wikidata project and you should defiantly catch me if you want to chat about linked data or something else!
