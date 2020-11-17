---
layout: post
title: Using SPARQL in QGIS
description: Introduction to the SPARQLing Unicorn QGIS plugin.
image: https://byabbe.se/assets/sparqling-unicorn-qgis.png
tags:
  - sparql
  - wikimedia
---

A couple of months back I discovered the [SPARQLing Unicorn](https://plugins.qgis.org/plugins/sparqlunicorn/) QGIS Plugin and it has been super useful for both data visualizations and Wikidata editing.

After installing it adds a new option under the "Vector" menu item in QGIS. Its interface allows one to access and query a set of predefined SPARQL endpoints including Wikidata as well as pointing to a custom endpoint or RDF file.

![screenshot](https://byabbe.se/assets/sparqling-unicorn-qgis.png)

One of my use cases has been to fetch [all glaciers in Wikidata missing GLIMS identifiers](https://w.wiki/mrC) and then add a GLMIS layer from the official Shapefiles so I can visually see the overlap.

![screenshot](https://byabbe.se/assets/qgis_sparql_compare.png)

I hope you will find this plugin useful as well.
