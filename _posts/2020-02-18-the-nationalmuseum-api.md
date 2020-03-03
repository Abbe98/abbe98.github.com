---
layout: post
title: The Nationalmuseum API
description: An introduction to the Nationalmuseum API.
image: https://byabbe.se/assets/natmus-vikus.png
tags:
  - museum
  - nationalmuseum
---
Nationalmuseum, the national gallery of Sweden has had an API for about two and a half year (I think) but it has yet to have any public documentation. So I decided to write down its features and some random tips.

### Capabilities

The API is able to return specific objects as well as returning all objects through pagination. Many objects also link to their external IIIF manifest.

### Retrieving an object

```
https://api.nationalmuseum.se/api/objects/4000
```
Check.

### Pagination through all objects

The API has two parameters for pagination `page` and `limit`. `limit` sets the number of objects you get per page the default is 50 and allowed values range from 1-100. 

Get the 100-200 objects\:
```
https://api.nationalmuseum.se/api/objects?page=2&limit=100
```
The response also returns you the URLs for the previous and next pages taking the limit parameter into account.

### Random notes

The URLs to items can seem daunting when you browse Nationalmuseums online collection but there is an alternative that's easy to link to with the identifier you get from the API\:
```
http://collection.nationalmuseum.se/eMP/eMuseumPlus?service=ExternalInterface&module=collection&viewType=detailView&objectId=24342
```

A great way to find interesting objects in the collection and connect it to other sources is to ask Wikidata\:
[Objects in Wikidata with Nationalmuseum IDs](https://w.wiki/HN3)

Finally for some insperation you could check out the [Nationalmuseum VIKUS Viewer instance](https://riksantikvarieambetet.github.io/VIKUS-Viewer-Nationalmuseum/).
