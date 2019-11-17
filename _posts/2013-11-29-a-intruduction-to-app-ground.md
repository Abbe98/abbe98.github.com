---
layout: post
title: A introduction to App Ground
description: A intruduction App Ground the optimized template for high end web apps.
image: https://byabbe.se/assets/default.png
tags:
  - code
---
On Github I describe [App Ground][1] as a "template/boilerplate for javascript/HTML5 web apps.". That's true but for most web apps App Ground is overkill. It uses things like AppCache, print styles and Open Graph.

I have often found myself adding all the stuff that's in App Ground to my basic HTML template when I starting on a new "advanced" web app. Some of these projects led to tons of optimizing, icons, offline support, speed, mobile support... I looked into projects as HTML5 Boilerplate and other templates, they're great but with one problem they doesn't approach apps in a scaling perspective. I believe in apps that scales from mobiles to big TV screens not just by provide native apps or mobile sites.

From that point of view I started working on App Ground. The first of August I did release the first stable version. On 4th August 1.0.1 was released after some fast feedback and discussions. But what features is in App Grounds 15 files?

### Features

### CSS

Normalize.css
[Normalize.css][2] is an alternative to CSS resets, it’s developed by Nicolas Gallagher. Normalize.css is also used by Twitter Bootstrap, HTML5 Boilerplate and many other big projects.

Print Styles

Print Styles in App Ground allows you to force page breaks, it also allows you to hide/view specific elements  when a user is printing a page. The print styles is provided by Facile Framework.

Help Classes

Help Classes is a collection of CSS classes you will use often, this includes classes to hide/view specific elements on different screen resolutions, align text and other common classes. Help Classes is also provided by Facile Framework.

### JS

jQuery

App Ground comes with [jQuery][3] 2.0.3 that supports major modern browsers. App Ground loads jQuery from the Google CDN, if it fails jQuery is loaded from a local copy.

Help JS

Help JS sets variables telling you if your user has a internet connection, a touch device,or is browsing your app in portrait or landscape mode and other things… Note that detecting touch devices does not work in some older browsers as Internet Explorer 9 Mobile(Windows Phone 7/7.5/7.8).

### Meta Tags

Open Graph

[The Open Graph Protocol][4](OGP) was developed at Facebook but it’s now supported by major search engines and social networks(Facebook, Google+, Google, Twitter, Bing…). It allows you to add images, types and other things to your meta data.

### AppCache

[AppCache][5] allows your user to browse your app when unable to connect to the internet. Remember you can use Help JS to detect when a user doesn't have a internet connection. Note that AppCache isn't supported by Internet Explorer 9.

App Ground have many other features that you can discover by browsing the code at [Github][6](the docs will be available soon). In the time of writing the latest version of App Ground is 1.1.1([CHANGELOG][7]).

[1]: https://github.com/Abbe98/App-Ground/
[2]: http://necolas.github.io/normalize.css/
[3]: http://jquery.com
[4]: http://ogp.me
[5]: http://www.w3.org/TR/offline-webapps
[6]: https://github.com/Abbe98/App-Ground/
[7]: https://github.com/Abbe98/App-Ground/blob/master/CHANGELOG.md
