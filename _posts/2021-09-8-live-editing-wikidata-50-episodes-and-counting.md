---
layout: post
title: Live Editing Wikidata&colon; 50 Episodes and Counting
description: Together with Jan Ainali I have now taken part in 50 episodes of Live Wikidata Editing. It's time for some reflection.
tags:
  - sparql
  - wikimedia
image: https://byabbe.se/assets/wikidata.png
---

It has been more than 17 months since [Jan Ainali][1] asked if I wouldn't be up for some live-streamed Wikidata editing. It seemed like an insightful and valuable thing to do. Now, over [50 episodes later][2], we have showcased more than 30 community tools, issued over 100 SPARQL queries, and even so, we don't lack ideas for future content.

### Tools Behind the Scenes

From day one, we have been using [StreamYard][3] and been broadcasting to a handful of platforms. Having no experience at all with streaming, StreamYard has been a joy to use. With a helping hand from Jan, I could get around the basics within a few minutes. Other tools I combine it with are [Wikimedia's URL-shortener][4] to easily share URLs and Firefox running a separate [profile][5] for the window I share. I often also have a separate [Joplin][6] window where I have notes and URLs I might need during the broadcast.

### Finding Content

While I personally could make 50 episodes of me editing historical railway systems and making maps with the same tools over and over, I try not to. I think three main things help us broaden our content beyond our own ideas.

#### 1. New community tools

Jan is particularly quick when it comes to picking up new tools that the community has come up with, I can't keep up myself and it has happened that I have showcased a tool as "new" when in fact it has been around for several years.

#### 2. Awareness days

Awareness days have been a great way to explore and edit new types of content. It's so useful that we even created an [awareness day calendar][7] using Wikidata and SPARQL on stream once.

#### 3. Events

There are plenty of themed events relating to Wikidata and Wikimedia which provide both content and new audiences for both us and the events.

### What Makes a Good Episode

Initially, I improvised and did everything live, and I still do that sometimes especially if I focus on editing/Wikidata content rather than on tools/workflows. An episode for which I have prepared a set of guiding points makes for better content. I guess my average preparation takes about 45 minutes. If I prepare or not depends much on if I find the time and motivation during the week. The most notable difference between a well-prepared episode and a less prepared one on my end is how many times I repeat the same things. Repeating something I just said is something I find myself doing when I improvise on the fly, if I, on the other hand, need to move straight to the next point the repetition does not occur.

Visual reusable examples and visualizations make <s>good</s> _popular_ content, while it appears like fancy graphs and maps draw the most viewers and views, just a few users picking up a powerful editing workflow or tool might be of much greater benefit to Wikidata and its community. We need a mix of these and I hope we got that mix.

The pace is tricky, especially when one does semitechnical things while one wants to give viewers the time to make comments. It's hit or miss on my end and I have yet to figure out a good way to manage it, especially as it's so dependent on the content.

### Things to Improve

#### 1. Backlog of Prepared Content

In the future, I would like to build up a "prepared content" backlog so that I can be confident in the quality even during weeks when I have a lot on my plate.

#### 2. Blog Posts Describing Advanced Workflows

It's not unusual that Jan or I share quite advanced workflows and while a stream might be a good way to showcase it, it might not be the best medium to help someone adopt it. I have once or twice created write-ups for showcased workflows but maybe what I should do is to do so before an episode so I can share it at the end of the stream.

#### 3. Ideas from the Community

Every now and then, we get a suggestion from the community for a topic or thing to talk about, but we could have more of this. No matter if you discover a tool that you found useful or if you made it, share it with us. We want to let more people know about it! [We should prompt this in more places.][8]

#### 4. Increase the interaction with viewers

One pattern I imagine I observe is that if one person makes a comment that we can bring up on screen it's more likely that someone else will too, even if it's just a "Hi!".

I'm yet unsure of what makes good content that encourages interactions with viewers. Maybe it's good old editing where we are far from experts on the data modeling we face so that the audience can suggest things that we can use and improve. Maybe we should talk more about the weather.

### Where You Find Our Episodes

We tend to stream on Saturdays at 20:00 UTC+2. The best way to get notified is by subscribing to the [Wikipedia Weekly Network on YouTube][9]. Our past episodes are listed over at the [Wikimedia Meta-wiki][2].

[1]: https://ainali.com/
[2]: https://meta.wikimedia.org/wiki/Wikipedia_Weekly_Network/Live_Wikidata_Editing
[3]: https://streamyard.com/
[4]: https://meta.wikimedia.org/wiki/Special:UrlShortener
[5]: https://support.mozilla.org/en-US/kb/profile-manager-create-remove-switch-firefox-profiles
[6]: https://joplinapp.org/
[7]: https://query.wikidata.org/#SELECT%20DISTINCT%20%3Fevent%20%3FeventLabel%20%3FeventTimestamp%20%28GROUP_CONCAT%28DISTINCT%20%3FsubjectLabel%3B%20separator%3D%27%2C%20%27%29%20AS%20%3Fsubjects%29%20WHERE%20%7B%0A%20%20VALUES%20%28%3Fmonth%20%3Fmonth_order%29%20%7B%0A%20%20%20%20%28%20wd%3AQ108%20%2701%27%20%29%0A%20%20%20%20%28%20wd%3AQ109%20%2702%27%20%29%0A%20%20%20%20%28%20wd%3AQ110%20%2703%27%20%29%0A%20%20%20%20%28%20wd%3AQ118%20%2704%27%20%29%0A%20%20%20%20%28%20wd%3AQ119%20%2705%27%20%29%0A%20%20%20%20%28%20wd%3AQ120%20%2706%27%20%29%0A%20%20%20%20%28%20wd%3AQ121%20%2707%27%20%29%0A%20%20%20%20%28%20wd%3AQ122%20%2708%27%20%29%0A%20%20%20%20%28%20wd%3AQ123%20%2709%27%20%29%0A%20%20%20%20%28%20wd%3AQ124%20%2710%27%20%29%0A%20%20%20%20%28%20wd%3AQ125%20%2711%27%20%29%0A%20%20%20%20%28%20wd%3AQ126%20%2712%27%20%29%0A%20%20%7D%0A%20%20%0A%20%20VALUES%20%3Fdays%20%7B%0A%20%20%20%20wd%3AQ18574943%0A%20%20%20%20wd%3AQ422695%0A%20%20%7D%0A%20%20%0A%20%20%3Fevent%20wdt%3AP31%2Fwdt%3AP279%2a%20%3Fdays%20.%0A%20%20MINUS%20%7B%20%3Fevent%20wdt%3AP31%20wd%3AQ57598%20%7D%0A%20%20%3Fevent%20wdt%3AP837%20%3Fday%20.%0A%20%20MINUS%20%7B%20%3Fevent%20wdt%3AP2894%20%5B%5D%20%7D%0A%20%20%3Fday%20wdt%3AP361%20%3Fmonth%20.%0A%20%20%3Fday%20p%3AP361%20%3Fmonth_statement%20.%0A%20%20%3Fmonth_statement%20pq%3AP1545%20%3Fday_of_month_rank%20.%0A%0A%20%20BIND%28IF%28xsd%3Ainteger%28%3Fday_of_month_rank%29%20%3C%2010%2C%20CONCAT%28%270%27%2C%20STR%28%3Fday_of_month_rank%29%29%2C%20STR%28%3Fday_of_month_rank%29%29%20AS%20%3Fday_of_month_rank_with_padding%29%0A%20%20BIND%28xsd%3AdateTime%28CONCAT%28STR%28YEAR%28NOW%28%29%29%29%2C%20%27-%27%2C%20STR%28%3Fmonth_order%29%2C%20%27-%27%2C%20STR%28%3Fday_of_month_rank_with_padding%29%2C%20%27T23%3A59%3A59%27%29%29%20AS%20%3FeventTimestamp%29%0A%20%20FILTER%28%3FeventTimestamp%20%3E%20NOW%28%29%29%0A%20%20%0A%20%20OPTIONAL%20%7B%20%3Fevent%20wdt%3AP921%20%3Fsubject%20%7D%0A%20%20OPTIONAL%20%7B%20%3Fevent%20wdt%3AP547%20%3Fcommemorates%20%7D%0A%20%20BIND%28IF%28%21BOUND%28%3Fsubject%29%2C%20%3Fcommemorates%2C%20%3Fsubject%29%20AS%20%3Fsubject%29%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%27%5BAUTO_LANGUAGE%5D%2Cen%27%20.%0A%20%20%20%20%3Fsubject%20rdfs%3Alabel%20%3FsubjectLabel%20.%0A%20%20%20%20%3Fevent%20rdfs%3Alabel%20%3FeventLabel%20.%0A%20%20%7D%0A%7D%20%0AGROUP%20BY%20%3Fevent%20%3FeventLabel%20%3FdayLabel%20%3FeventTimestamp%0AORDER%20BY%20%3FeventTimestamp
[8]: https://meta.wikimedia.org/w/index.php?title=Wikipedia_Weekly_Network%2FLive_Wikidata_Editing&type=revision&diff=21991439&oldid=21991036
[9]: https://www.youtube.com/c/WikipediaWeekly
