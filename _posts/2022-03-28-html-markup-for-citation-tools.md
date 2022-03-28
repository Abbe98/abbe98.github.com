---
layout: post
title: HTML Markup for Citation Tools
description: I show some of the HTML markup needed for your web pages to support tools like Zotero and Citioid.
tags:
  - code
  - tips
---

Isn't it great when a citation tool like Zotero or Wikipedia's Citoid takes a link and turns it into a citation? In this post, I show some of the HTML markup needed for your web pages to support just that.

### How Zotero and Citoid works

The most common citation tools out there are just like Citoid and Zotero powered by [Zotero-translators](https://github.com/zotero/translators/), a set of JavaScript files that parse web pages into citations using things like XPath and CSS selectors.

### Let's make your site work with citation tools

Now you could write a Zotero-translations file for your site and submit it. There are already over 600 ones that could serve as examples. That might be a good way forward if you don't have control over your website's HTML markup.

However, one of those Zotero-translators files, "[Embedded Metadata.js](https://github.com/zotero/translators/blob/master/Embedded%20Metadata.js)" happens to be a generic one that will try to extract data from your site if it does not have its own translator.

That translator is very capable and supports both common and generic metadata ontologies such as Open graph and ones one mostly find in industry-specific settings like BibO and Eprint Terms.

### The tags and attributes your page needs

These tags are the ones I have ended up using as they are rather generic and serve many use-cases beyond citation. 

<pre><code class="language-html">&lt;link rel="canonical" href="https://byabbe.se/example-page"></code></pre>
Always include a canonical tag! That ensures that the link used is your canonical link and not the one copied or visited by the user.


<pre><code class="language-html">&lt;meta property="og:title" content="Not your page title"></code></pre>
The title of the work or article is not necessarily the same as the page title, as the latter can contain things like the site name.

<pre><code class="language-html">&lt;meta name="author" content="Albin Larsson"></code></pre>
The name of the author.

<pre><code class="language-html">&lt;meta property="og:site_name" content="Site name"></code></pre>
The name of the site.

<pre><code class="language-html">&lt;meta property="og:article:published_time" content="2022-02-03T00:00:00+00:00"></code></pre>

Time of publication, note that this is from the article namespace in the Open Graph vocabulary. Let me know if you find a more generic property that is as widely supported!

<pre><code class="language-html">&lt;html lang="en"></code></pre>

Language of the page.

<pre><code class="language-html">&lt;meta name="description" content="An actual description."></code></pre>

A description of the work, this isn't commonly used for display purposes but some tools/setups still use it for indexing, etc.


Do you have other markup you use to expose data to citation tools? [Let me know!](https://byabbe.se/)
