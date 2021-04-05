---
layout: post
title: Weekly Update 2
description: Rendering the Milky way with WebGL in full 3D will be easy when I got a supercomputer.
image: https://byabbe.se/assets/default.png
tags:
  - other
---
Another week and a overkill experiment. So the "huge" space and WebGL related project that I did mention in the [last update][1], was just to huge.

I got the idea some months ago when I was in Gothenburg, I played around whit a program that visualized the known universe as a particle map and allowed you to browse it in 3D with a Xbox control It blew my mind, not because it was cool but because it shouldn't be hard to do the same thing with WebGL. The same evening I searched for the data needed. I couldn't find it and dropped the idea.

Until last weekend when I did send email to the NASA asking about the data, I haven't got a answer yet and I don't except one. I did start digging into available sources and what people had done before, and I found that some one had already created a [particle map over the Milky way][2](a Chrome experiment) so rendering universe as a particle map was no longer anything to cool. But rendering it by scale in full 3D would still be cool. After some evil data mining I had data about 150 000 stars, location size and type. I did a test, and rendered 10 stars to see if my code worked as excepted(it did after some errors) and both texture and lightning as well. So then I added all data, and to make a long story short can anyone remind me of this projects when we can put supercomputers in every humans hands?

[1]: https://byabbe.se/2014/02/28/weekly-update-1
[2]: http://workshop.chromeexperiments.com/stars/