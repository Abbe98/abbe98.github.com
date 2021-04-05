---
layout: post
title: KSamsok PHP Advanced Usage
description: Learn how to work with Swedish Heritage data in PHP with this advanced example.
image: https://byabbe.se/assets/soch-logo.jpg
tags:
  - soch
  - code
---

This is the second part out of two introducing the KSamsok-PHP API library, the first part is [KSams&ouml;k-PHP: the Basics](https://byabbe.se/2016/01/25/ksamsok-the-basics/).

### Extending

When KSams&ouml;k-PHP does not have a method for a request you want to preform against the K-Sams&ouml;k API extending KSams&ouml;k-PHP might be the solution. Extending KSams&ouml;k-PHP allows you to use KSams&ouml;k-PHP functions for formating URIs, validate responds, parsing and more, together with your own custom requests.

Extending the `kSamsok` class gives your new child class access to a set of protected methods useful to you.

<pre class="line-numbers"><code class="language-php">customKSamsok extends kSamsok {
  // your custom methods
}</code></pre>

In the following example we will write a method for retrieving the first 250 photos of the media type `image/jpeg`, that has thumbnails based on a text-based search string. Note that KSams&ouml;k-PHP can only parse the presentation format so make sure you always append `&recordSchema=presentation`.

### Preparing the URL

The `prepareUrl()` deals with encoding/whitespace in your URL and make sure it's valid, always use it! Note that we access the API key with `$this->key` and the endpoint with `$this->url`.

<pre class="line-numbers"><code class="language-php">customKSamok extends kSamsok {
  public function photoSearch($text) {
    $url = $this->url . 'x-api=' . $this->key . '&method=search&hitsPerPage=250&query=itemType="Foto"%20and%20text="' . $text . '"%20and%20mediaType="image/jpeg"%20and%20thumbnailExists=j&recordSchema=presentation'; // build the URL

    $url = $this->prepareUrl($url); // Fix possible encoding/whitespace issues
  }
}</code></pre>

### Validating the Response

`validResponse()` validates a response, returning `false` if the resource is inaccessible or broken.

<pre class="line-numbers"><code class="language-php">customKSamok extends kSamsok {
    public function photoSearch($text) {
      $url = $this->url . 'x-api=' . $this->key . '&method=search&hitsPerPage=250&query=itemType="Foto"%20and%20text="' . $text . '"%20and%20mediaType="image/jpeg"%20and%20thumbnailExists=j&recordSchema=presentation'; // build the URL 

      $url = $this->prepareUrl($url); // Fix possible encoding/whitespace issues
      
     if (!$this->validResponse($urlQuery)) { // return false if record is inaccessible
       return false;
     }
   }
}</code></pre>

### Parsing the Results

KSams&ouml;k-PHP parses each item(record) one by one as a SimpleXMLElement object using its `parseRecord()` method. Note the use of `killXmlNamespace()`.

<pre class="line-numbers"><code class="language-php">customKSamok extends kSamsok {
    public function photoSearch($text) {
      $url = $this->url . 'x-api=' . $this->key . '&method=search&hitsPerPage=250&query=itemType="Foto"%20and%20text="' . $text . '"%20and%20mediaType="image/jpeg"%20and%20thumbnailExists=j&recordSchema=presentation'; // build the URL 

      $url = $this->prepareUrl($url); // Fix possible encoding/withespace issues

     if (!$this->validResponse($urlQuery)) { // return false if recorce is inaccessible
       return false;
     }

     $xml = file_get_contents($url); // get the resource contents
     $xml = $this->killXmlNamespace($xml); // bypass XML-Namespaces for the SimpleXMLElement class
     $xml = new SimpleXMLElement($xml); // create the SimpleXMLElement object

     $result[] = array(); // array container for the parsed items
     foreach ($xml->records->record as $item) { // loop through all the items
       $result[] = $this->parseRecord($item); // push parsed item to result array
     }

     return $result;
   }
}</code></pre>

### Usage

Using your new method is now as easy as using any of the basic ones\:

<pre class="line-numbers"><code class="language-php">$kSamsok = new customKSamok('test');
$searchResultArray = $kSamsok->photoSearch('kyrka');</code></pre>

Now have fun and build something, checkout the [Documentation](https://byabbe.se/ksamsok-php/) and report any evil bugs at [Github](https://github.com/Abbe98/ksamsok-php).

Previous posts about K-Sams&ouml;k and heritage data\:

 - [KSams&ouml;k-PHP\: the Basics, January 2016](https://byabbe.se/2016/01/25/ksamsok-the-basics/)
 - [Enabling CORS in SOCH with a Proxy on Google App Engine, November 2015](https://byabbe.se/2015/11/24/enabling-cors-in-soch-with-a-proxy-on-google-app-engine/)
 - [Mapping the Past with Linked Data in OpenHistoricalMap, Mars 2015](https://byabbe.se/2015/03/26/mapping-the-past-with-linked-data-in-openhistoricalmap/)
 - [Mapping the Past with OpenHistoricalMap and JOSM, Mars 2015](https://byabbe.se/2015/03/03/mapping-the-past-with-openhistoricalmap-and-josm/)
 - [Holiday Project K-Sams&ouml;k, January 2015](https://byabbe.se/2015/01/07/holiday-project-ksamsok/)
