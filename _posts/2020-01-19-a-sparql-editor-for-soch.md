---
layout: post
title: A SPARQL Editor for SOCH
description: In this post I'm introducing a custom SPARQL editor for K-samsök.
image: https://byabbe.se/assets/soch-sparql.png
tags:
  - soch
---

![screenshot of the editor](https://byabbe.se/assets/soch-sparql.png)

About a year ago I made a custom SPARQL editor for the Swedish Open Cultural Heritage (SOCH/K-samsök) LOD platform since then it has served me, both at home and at the office. Now I'm hosting an instance for anyone to use. It was built both to aid me (and others) working with the over 8 million RDF records in SOCH as well as to be a prof of concept and reference for future work.

The editor comes with a ton of features including:

 - Autocompletion of the entire SOCH ontology
 - Autocompletion of some external endpoints, including Wikidata and Europeana
 - Result visualizations, including a table, an image grid and a pie chart
 - Integration with a query library
 - Shareable queries
 - A resizable code editor
 - An interactive tour of its GUI

There is no official SPARQL endpoint for SOCH so the first time you uses the editor you will be asked to enter your own endpoint or a third party one.

[You can find the editor here](https://byabbe.se/thor/) and yes it's inspired by the WDQS GUI.

**How to setup a SPARQL endpoint with SOCH data?**

First I usually bulk download RDF records with [SOCH download CLI](https://github.com/riksantikvarieambetet/SOCH-download-CLI). Secondly I load these into [Fuseki](https://jena.apache.org/documentation/fuseki2/) (super easy to setup, but somewhat low performance if you load all of SOCH into it) or [Blazegraph](https://blazegraph.com/) (trickier to setup but great performance).
