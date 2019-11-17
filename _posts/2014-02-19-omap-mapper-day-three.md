---
layout: post
title: OMap Mapper day three
description: The OMap Mapper project day three, some UI stuff and a Mozilla joke.
image: https://byabbe.se/assets/default.png
tags:
  - omapmapper
---
Now most of the boring stuff is done, all validation works and the select location is ported to JavaScript, not all the a11y related stuff but it works. It will be quite inaccessible anyway because I don't deal with all the auto focus that a JavaScript based UI would need.

The only problem I was running into was the cursor used by Leaflet, it uses the move cursor for all browsers except Opera, Chrome and Firefox, for those browsers it's using grab/grabbing both grab and grabbing is not a part of the CSS standard and requires prefixes to be used. So when change the cursor during the select location function I can't later change it back in Firefox/Opera/Chrome in a nice way. So I was forced to set the default cursor to move. Nothing bad in that but it doesn't look just as smooth.

I should also add that all the marker/map/icons animations makes the UI a bit slow, no problem on most computers but I tested on a older one(6 years but upgraded) so adding a option to disable that is something I could consider in the future(The blue sky(Mozilla style)). ;-)

Responsive design is also in the blue sky :P