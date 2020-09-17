---
layout: post
title: Getting Random Results in SPARQL
description: I explain how to get random results from a SPARQL endpoint and why it is as tricky as it is.
tags:
  - sparql
---
Just the other day I decided to take a stab at [an old StackOverflow questing about getting random results from SPARQL](https://stackoverflow.com/questions/5677340/how-to-select-random-dbpedia-nodes-from-sparql/63909084#answer-63909084).

The most obvious solution might first appear to be using SPARQL's built-in `RAND()` function and order by that random number:

<pre><code class="language-sparql">SELECT ?s WHERE {
  ?s ?p ?o .
  BIND(RAND() AS ?random) .
} ORDER BY ?random
LIMIT 1</code></pre>

This could have been perfectly fine if it weren't for SPARQL engines trying to be smart and statically evaluating the third line. At the second result row, most SPARQL engines see a line and "thinks", "oh this is identical to what I did on the row before this one, the result must be the same".

This can be illustrated by the Wikidata SPARQL query below, note how all rows have the same `?random` value:

<pre><code class="language-sparql">SELECT ?item ?itemLabel ?random WHERE {
  ?item wdt:P31 wd:Q11762356 .
  BIND(RAND() AS ?random) .
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE], en" . }
} ORDER BY ?random
LIMIT 100
# comment, change this before each run to bypass WDQS cache</code></pre>

A common solution to this issue is ditch `RAND()` entirely and instead hash a value in each row and sort it by the hash.

<pre><code class="language-sparql">SELECT ?s WHERE {
  ?s ?p ?o .
  BIND(MD5(?s) AS ?random) .
} ORDER BY ?random
LIMIT 1</code></pre>

This will however generate the same order each time as the hashes are entirely based on the result data. Illustrated by the example below:

<pre><code class="language-sparql">SELECT ?item ?itemLabel ?random WHERE {
  ?item wdt:P31 wd:Q11762356 .
  BIND(MD5(STR(?item)) AS ?random) .
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE], en" . }
} ORDER BY ?random
LIMIT 100
# comment, change this before each run to bypass WDQS cache</code></pre>

The solution is to combine the two. The use of hashed result data makes sure the SPARQL engine can't statically evaluate `RAND()` and the fact that `RAND()` is therefore executed each time helps avoid the selection bias.

<pre><code class="language-sparql">SELECT ?s WHERE {
  ?s ?p ?o .
  BIND(SHA512(CONCAT(STR(RAND()), STR(?s))) AS ?random) .
} ORDER BY ?random
LIMIT 1</code></pre>

Here again illustrated with a Wikidata query:

<pre><code class="language-sparql">SELECT ?item ?itemLabel ?random WHERE {
  ?item wdt:P31 wd:Q11762356 .
  BIND(SHA512(CONCAT(STR(RAND()), STR(?item))) AS ?random) .
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE], en" . }
} ORDER BY ?random
LIMIT 100
# comment, change this before each run to bypass WDQS cache</code></pre>

Know a better way to retrieve random results from SPARQL? [Let me know on Twitter!](https://twitter.com/AlbinPCLarsson)