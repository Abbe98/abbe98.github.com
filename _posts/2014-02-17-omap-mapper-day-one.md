---
layout: post
title: OMap Mapper day one
description: The OMap Mapper project day one, web a11y and maps.
image: https://byabbe.se/assets/default.png
tags:
  - omapmapper
---
So first day with my new OMap Mapper project, and it has been great weather all day, for short I haven't done so much on the application. Still some major things is done.

![Screenshot from OMap Mapper][1]
Here is the layout I'm aiming for, a `<nav>`, `<aside>` and some dark boring buttons, but they light up when you got focus or hover them :-P If you have seen some other CSS stuff that I have made to, you might know that I got my evil transitions there to.

    * {
	  -webkit-transition: .4s;
	  -moz-transition: .4s;
	  transition: .4s;
    }

I did also choose to use the [Leaflet.markercluster][2] plugin, and I decided that I wont use [mustache.js][3] right now, I did play with it and it will not be any problem adding it later if I feel for it.

I did also write the PDO class that I'm going to used, it's based on the one that I'm using all the time([Gist][4]).

I did get I question about how I would handle the location input needed using Leaflet, I will just do it the way I'm always doing it:

    <label>Location: <input type="text" value="" class="hide" name="location" /><button>Choose Location</button></label>
    
I have a jQuery wrapper that I'm using all the time but this time I will rewrite it to pure JS. It's quite easy to explain, the text input is hidden by CSS, when the button is clicked the user can click somewhere on the map, the location will be added to the text inputs value, and the state of the button will change.

Just some accessibility thing to think of when using this solution:

 - Don't hide the text input on screen readers(adds another input possibility)!
 - When the button is clicked change focus to the map!
 - Allow the user to change the location from the button!
 - Don't use the `application` role on the map!

I might actually write a blog post about maps and web accessibility, it's interesting subject :-)

That's it right now.
 
[1]: https://byabbe.se/assets/omapmapper2.jpg
[2]: https://github.com/Leaflet/Leaflet.markercluster
[3]: https://github.com/janl/mustache.js
[4]: https://gist.github.com/Abbe98/8862278
