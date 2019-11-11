---
layout: post
title: Holiday Project K-Samsök
description: Showing off my holiday project that is using open data.
image: https://byabbe.se/assets/bildplats.png
---
My Christmas holiday started with me becoming sick, a terrible thing for the planned orienteering and workouts. So I decided to go for a little bigger holiday project the usually.

I have for a long time wanted to build something real with the K-samsök(SOCH) API, a API containing more then 5.6 million historical/archeology objects, including 2.3 million images and 1.6 million geo referenced objects.

Earlier last year I started working on a PHP library for the API, you will find the latest version at [Github][0] and [Packagist][1]. It's written in PHP because I think more people will use it. You find some basic documentation in the README, some features such as `object()`, extending, and optional parameters is missing. I aim to publish 1.0 when the documentation is complete. 

Until this holiday it has been very unstable and has been missing some key functionality. The best solution to make a library stable is to build something with it, so that's what I have been doing.

169 000 of the images in K-Samsök are geo referenced the other ones is not. Many of the other images is photos. I have written a web app that allows you to search after photos thats isn't geo referenced and simply geo reference using a location picker. A screenshot can be seen below.

![Screenshot from the app][3]

The screenshot lies, it's a week old but it's still just as nice!

Most of the work is done, but some features is still missing:

 - The own API for getting the user generated data.
 - Scaling, the UI is powered by a lot of JS and its needs work.
 - It should be more accessible to screen reader/keyboard users, the JS breaks it right now.

The aim was to "finish" it until the end of this holiday, but school begins tomorrow. The new aim is to finish it and 1.0 of K-samsök-PHP before the [Wiki Loves Maps Hackathon][4] in February!

[Here is the source for the K-Sams&ouml;k statics.][5]

[0]: https://github.com/Abbe98/ksamsok-php
[1]: https://packagist.org/packages/abbe98/ksamsok-php
[3]: https://byabbe.se/assets/bildplats.png
[4]: http://wikilovesmaps.wikimedia.fi/
[5]: http://www.k-blogg.se/2014/12/23/k-samsok-2014-tio-punkter/