---
layout: post
title: Mapping the Past with Linked Data in OpenHistoricalMap
description: OpenHistoricalMap is a great place, for open linked data, it has some advantages over other data platforms and some disadvantages.
image: https://byabbe.se/assets/himlinge-sunset.jpg
tags:
  - openhistoricalmap
---
**Extended 2015/03/29**

OpenHistoricalMap is a great place for open linked data, it has some advantages over other data platforms and some disadvantages. 

The main advantage is that the OpenStreetMap(/OpenHistoricalMap) platform is open enough to be **extensible for all other open platforms** and even closed ones.

The main disadvantage is that the platform is actually not a good place for the data itself, it works great as long it's physical descriptions such as `end_date`/`name`/`building:levels` etc but for other data such as lists/images/stories OpenHistoricalMap is not the solution you should use.

Luckily for us linked data works great across platforms and that is why OpenHistoricalMap is a great place for your linked data. OpenHistoricalMap can easily link to platforms such as Wikidata, Wikipedia, Europeana and SOCH. Which are great for other types of data.

### How I do Linked Data in OpenHistoricalMap

Currently there is no "standard solution" for linked data I have seen concepts using extensions such as RDF and JSONLD. Personally I'm not a huge fan of any of them because they are complex and requires additional implantations.

I do linked data in OpenHistoricalMap with only URIs as values and key namespaces this can mean many(many many) keys but it does not require format extensions. 

For my experiments/prof of concept I use the [City wall of Visby](http://www.openhistoricalmap.org/way/198179683) because I will have no issues linking tons of data to it.

First of we got Wikipedia articles we want to link to from our object in OpenHistoricalMap. Using my linked data schema this would be a `description` of the object but OpenStreetMap(/OpenHistoricalMap) do already have a key for Wikipedia so we should use it(`wikipedia:langcode`).

Wikipedia is the only platform that OpenStreetMap(/OpenHistoricalMap) has a custom key for.

For links to other platforms I use the key `uri` because `uri` should't exist in OpenStreetMap I use it as an key namespace of the `ohm` key: `ohm:uri`. 

Then I'm defining how this is related to the OpenHistoricalMap object for example:

 - `ohm:uri:is_described_by`
 - `ohm:uri:is_described_as`
 - `ohm:uri:is_visualised_by`
 - `ohm:uri:is_mentioned_by`
 - `ohm:uri:consists_of`
 - `ohm:uri:is_part_of`
 - `ohm:uri:is_related_to`
 - `ohm:uri:contains`
 - `ohm:uri:same_as`

Now I use another namespace to tell what platform the link goes to as not all applications would support each platform:

 - `ohm:uri:is_related_to:soch`
 - `ohm:uri:is_related_to:europeana`
 - `ohm:uri:is_described_by:wikidata`
 - `ohm:uri:is_related_to:some_other_platform`

Platforms might support different file formats so we need a namespace for the format too:

 - `ohm:uri:is_related_to:soch:jsonld`
 - `ohm:uri:is_related_to:soch:platform_uri`
 - `ohm:uri:is_related_to:soch:xml`
 - `ohm:uri:is_related_to:soch:rdf`

This value should be the filename extension of the format or `platform_uri`(platform internal URI) a web page representation would for example have the format `html` not `php` or `asp` etc because the end user format is HTML.

That's it when it comes to the key and its namespaces, sometimes a namespace for time duration would make sense too.

### Links Between Objects in OpenHistoricalMap

Linking between objects in OpenHistoricalMap could use the same approach: `ohm:uri:contains:openhistoricalmap:platform_uri` would be a valid key. The platform URI then states if it's a relation,  node, or way followed by the object id(for example `n2083278729`). 

### Example

As a showcase and proof of concept I have been adding `ohm:uri`s to [the Visby city wall](http://www.openhistoricalmap.org/way/198179683#map=16/57.6414/18.2934&layers=HN). Data from the following platforms are linked in this example:

 - SOCH
 - Europeana
 - OpenStreetMap
 - OpenHistoricalMap
 - Wikidata
 - Wikimedia Commons
 - Platsr
 - Wikipedia(using the `wikipedia` key)

Totally(in the time of writing) I have 16 URIs linked, does not seams like it's much information? 

It's ton of useful data, both SOCH, Wikipedia, Platsr, and Europeana has own relations and linked data for this example. Wikipedia contains hundreds related and relevant links, SOCH has many high quality links and user generated ones.

This allows users to find more information, then possible just by searching Google and it allows developers to integrate with the data and build rich user experiences. 

Related reading over at the OpenStreetMap Wiki:

 - [Semi-colon Value Separator](https://wiki.openstreetmap.org/wiki/Semi-colon_value_separator)
 - [Namespace](https://wiki.openstreetmap.org/wiki/Namespace)

I'm only saying that this is how I do linked data in OpenHistoricalMap feedback and criticism is loved.  Will document everything over at the Wiki in the coming week.

### Extended

**This part was first published at the OpenHistoricalMap mailing list. It might contain duplicate information.**

#### ohm:

This is to make sure that it never gets confused with tags in OSM, I think all custom tags should have this namespace. OHM uses the same software as OSM for APIs, database, even frontend there for we should protect each project. We using the same editing software, data will end up in the wrong place... But yes it could be removed.

#### uri:

A relation using this approach will always be a URI, also it makes sense to have all relations under at least one common tag. But it could be removed, but it would be easier to query with a common uri tag...

#### relation:

This one is the core, I made up a few, that would make sense for OHM. This one can't be removed(and we have no reason to do so).

#### platform:

To get/parse data we need to know what it looks like, different platforms has different APIs and data models. The sooner we tell the developers what platform they should query for a specific relation the better. Just a URI does not make sense as many URIs are just id numbers.

#### format:

Sending a HTTP request to a URL would give us the format but lets say that an object in OHM has 200 URLs linked. Would we send 200 HTTP requests to get the format so we could see which ones we can support? Some URL formats would tell us the format(`http://kulturarvsdata.se/shm/object/xml/974121`is xml), but not all does... 

It's about both be nice to developers and mappers, this approach can be used by both. 

Platform specific RDF namespaces such as EDM would work for platforms that are big with linked data, such as SOCH, but for all other platforms? Having one solution working for all platforms is a advantage.

We should of curse care about RDF and platform specific RDF namespaces, but the way to do it is maybe through middleman libraries/services(LdRequest->requestParsing->Overpass->RdfParsing->RdfResponse)? This way we could support common LD platforms and non LD ones. such a service could be self hosted or available as a API.

The relation/platforms/format should be documented, and such documentation could be available in RDF format(and any other LD format). It would even be a great idea to set up a OHM RDF namespace to be able to provide RDF output.

OHM can't wait for all other platforms to do linked data, this approach allows OHM to do linked data now with any open platform.