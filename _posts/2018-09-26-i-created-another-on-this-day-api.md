---
layout: post
title: I Created Another On this Day API
description: There are multiple "On this Day" APIs built on top of Wikipedia but I created yet another one. This API can be used to retrieve birth, deaths, and events for any given day of the year.
image: https://byabbe.se/assets/screenshot-on-this-day-api-docs.png
---

![screenshot of documentation](https://byabbe.se/assets/screenshot-on-this-day-api-docs.png)

There are multiple "On this Day" APIs built on top of Wikipedia but I created yet another one. This API can be used to retrieve birth, deaths, and events for any given day of the year.

The reason for building this was that I wanted something stable with support for things like Cross-Origin-Requests and SSL. The need wasn't actually mine. A friend of mine sees the potential of "On this Day" information as a possible delighter in everyday contexts and I offered to help.

The data is (because it's harvested from Wikipedia) licensed under [Creative Commons Attribution-ShareAlike 3.0 Unported](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License) The API is actually just a collection of pre-generated static JSON files cached and exposed using Cloudflare. So feel free to query without limits.

[API Sandbox and Documentation](https://byabbe.se/on-this-day/)
