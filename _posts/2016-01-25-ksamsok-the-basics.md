---
layout: post
title: KSamsok PHP the Basics
description: Learn how to work with Swedish Heritage data in PHP.
image: https://byabbe.se/assets/soch-logo.jpg
tags:
  - soch
  - code
---

K-Sams&ouml;k also known as SOCH is an aggregator and API for Swedish culture heritage institutions, it's developed by the [Swedish National Heritage Board](http://www.raa.se/om-riksantikvarieambetet/in-english/) and in the time of writing it has 6,066,262 items indexed.

 - 2,660,852 items has images
 - 1,612,261 items has coordinates
 - 628,582 media items has a public domain like license
 - 2,929 items are maps
 - and there is tons of linked data in there

Because content APIs that default to RDF sucks(I love linked data but still), messy URIs sucks and because K-Sams&ouml;k got amazing content I wrote this API library.

Ksams&ouml;k-PHP links\:

 - [Documentation](https://byabbe.se/ksamsok-php/)
 - [Github](https://github.com/Abbe98/ksamsok-php)
 - [Packagist](https://packagist.org/packages/abbe98/ksamsok-php)

### Installing

Installing K-Sams&ouml;k PHP requries the Composer package manager\:

`composer require abbe98/ksamsok-php`

### Initialize

K-Sams&ouml;k requires an API key, for messing around you can use `test`. Create a new instance of the `KSamsok` class and provide your API key\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');</code></pre>

### Making a Simple Text Search

Making a text based search is done using the the search method\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$searchResultArray = $kSamsok->search('kanon', 1, 60);</code></pre>

Oh, parameters! The first one(`'kanon'`) is the string to search for, the second parameter defines where in the results you want to start retrieving items for example `1` means you want to start from the beginning of the search results. The last parameter in the example above tells the API how many items you want to retrieve(1-500 is valid).

The following example would result in a search for the string `kyrka` starting at result 60 retrieving 60 results\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$searchResultArray = $kSamsok->search('kyrka', 60, 60);</code></pre>

There is an optional parameter too\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$searchResultArray = $kSamsok->search('kyrka', 60, 60, true);</code></pre>

This would simply make the something as the last example but only request items whit images, neat isn't it?

Okay, that's a basic text based search, lets move on.

### Autocompleting Search

K-Sams&ouml;k has a simple method for auto completing and it's super simple to use with KSams&ouml;k-PHP\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$searchHintObject = $kSamsok->searchHint('ka', 3);</code></pre>

The first `searchHint()` parameter is the string to get auto completing suggestions from, the second parameter is optional and sets the number of suggestions to retrieve the default value is `5`. So now you can actually create a basic search engine.

### Searching within a Bounding Box

Now lets check out the KSams&ouml;k-PHP method for making bounding box searches\:

<pre class="line-numbers"><code class="language-php">$west = '16.41';
$south = '59.07';
$east = '16.42';
$north = '59.08';

$kSamsok = new KSamsok('test');
$bBoxResultsArray = $kSamsok->geoSearch($west, $south, $east, $north, 300, 500);</code></pre>

The parameters should be quite straight forward the four first parameters define the lat/lon borders of the bounding box. The first integer parameter does define where in the results to start retrieving items the last parameter define how many results to retrieve(1-500 is valid).

The remaining public methods of KSams&ouml;k-PHP uses URIs as the main parameter so first let me introduce you to URIs in K-Sams&ouml;k. Lets take a look at the following URI\: `raa/kmb/16000300020896` This is the most "raw" URI you can get in K-Sams&ouml;k. First the data provider is defined and then there is a regular ID.

To retrieve the XML source of this item(from the API) you would guess there would be some parameter or extention such as `raa/kmb/16000300020896.xml` or `raa/kmb/16000300020896?format=xml`. This is actullay how it's done\: `raa/kmb/xml/16000300020896`.

This results in the fact that items URIs and URLs is somewhat diverse\:

- `raa/kmb/16000300020896`
- `raa/kmb/xml/16000300020896`
- `raa/kmb/rdf/16000300020896`
- `raa/kmb/html/16000300020896`
- `http://kulturarvsdata.se/raa/kmb/16000300020896`
- `http://kulturarvsdata.se/raa/kmb/xml/16000300020896`
- `http://kulturarvsdata.se/raa/kmb/rdf/16000300020896`
- `http://kulturarvsdata.se/raa/kmb/html/16000300020896`

Yep that's the same item. In KSams&ouml;k-PHP it does not matter what URI or URL you provides it handles it for you out of the box!

### Getting a Single Item

Lets return a single item based on its URI or URL\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$itemObject = $kSamsok->object('http://kulturarvsdata.se/shm/site/xml/18797');</code></pre>

The following example would return the same result\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$itemObject = $kSamsok->object('shm/site/18797');</code></pre>

### Getting Items Relations

Returning all relations for a item is just as neat\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$relationsObject = $kSamsok->relations('shm/site/18797');</code></pre>

Now we only have one public method left and it's `uriFormat()`. `uritFormat()` convert K-Samsök URIs and URLs to any URI/URL type and even validate them\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new KSamsok('test');
$uriString = $kSamsok->uriFormat('shm/site/18797', 'xmlurl');</code></pre>

This would result in the string `http://kulturarvsdata.se/shm/site/xml/18797` being returned. The first parameter is simply the item URI or URL. The second parameter sets the type of URI or URL to be returned([see the documentation](https://byabbe.se/ksamsok-php/#uri)). By setting a third optional parameter to `true` you can trigger validation of the URI(returns `false` if invalid).

That's the basic usage of KSams&ouml;k-PHP in part two we extend its features using its protected methods to be able to take advantage of all K-Sams&ouml;ks powerful native methods.

Previous posts about K-Sams&ouml;k and heritage data\:

 - [Enabling CORS in SOCH with a Proxy on Google App Engine, November 2015](https://byabbe.se/blog/2015/11/24/enabling-cors-in-soch-with-a-proxy-on-google-app-engine/)
 - [Mapping the Past with Linked Data in OpenHistoricalMap, Mars 2015](https://byabbe.se/blog/2015/03/26/mapping-the-past-with-linked-data-in-openhistoricalmap/)
 - [Mapping the Past with OpenHistoricalMap and JOSM, Mars 2015](https://byabbe.se/blog/2015/03/03/mapping-the-past-with-openhistoricalmap-and-josm/)
 - [Holiday Project K-Sams&ouml;k, January 2015](https://byabbe.se/blog/2015/01/07/holiday-project-ksamsok/)