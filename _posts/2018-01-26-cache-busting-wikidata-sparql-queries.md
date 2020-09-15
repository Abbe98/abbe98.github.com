---
layout: post
title: Cache Busting Wikidata SparQL Queries
description: Whenever you write a Wikidata query form which you do not expect the result to be the same each time, you will run into the issue of caching.
image: https://byabbe.se/assets/wikidata.png
tags:
  - wikimedia
---

**UPDATE:** By setting a `cache-control: no-cache` header you can disable this query caching.

### The problem

Whenever you write a Wikidata query form which you do not expect the result to be the same each time, you will run into the issue of caching. Lets take the following example, returning a random cat\:

<pre><code class="language-sparql">SELECT ?item ?itemLabel (MD5(CONCAT(STR(?item), STR(RAND()))) as ?random)
WHERE 
{
  ?item wdt:P31 wd:Q146.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE], en". }
} ORDER BY ?random 
LIMIT 1
</code></pre>

[Run in the Wikidata Query Editor](http://tinyurl.com/yd4cpfrn)

If you run this once you will get a random cat if you run this twice you will get the same random cat. 

This is because Wikidata has saved the result, to serve you faster the second time.

### The Solution

A solution some people uses is to "just add a space somewhere", this is possible because Wikidata cache queries based on the SparQL string, not the actual parsed and preformed query.

When used in implementations keeping track of spaces is not an option so I decided to use random comments that could be generated from hashing functions etc\:

<pre><code class="language-sparql">#01e8c03a6bdfe392431d8189130fcfc0
SELECT ?item ?itemLabel (MD5(CONCAT(STR(?item), STR(RAND()))) as ?random)
WHERE 
{
  ?item wdt:P31 wd:Q146.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE], en". }
} ORDER BY ?random 
LIMIT 1
</code></pre>

Changing the comment string and rerunning the query will result in an new random cat.

When actually used in real world implementations where you might minify your queries I suggest appending the comment just before preforming it.

### Final Notes

 - This is not actual cache busting, it's a way to avoid the cached response.
 - The "random item" example available in the Wikidata Query Editor previously used the `SHA512` function and not the `MD5` one used in my examples. I have updated the example because the `MD5` function preforms about five times as fast.
