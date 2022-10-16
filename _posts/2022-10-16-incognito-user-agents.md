---
layout: post
title: Incognito User Agents
description: Me rambeling about incognito user agents.
tags:
  - privacy
---
User Agent spoofing isn't news and is necessary for many Internet users. Today, however, I noticed something I hadn't earlier. User  Agent spoofing causing analytics and security services to report the wrong operating system and browser altogether.

I logged into Twitter from GNOME Web on a PostmarketOS device, and the login notice I received a while later told me I had logged in from an Android device using Google Chrome.

`Mozilla/5.0 (Linux;Android 10; Pixel) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.96 Mobile Safari/537.36`

It turns out that GNOME Web doesn't expose Linux distro or what browser I'm using by default. That's all good, as it reduces the ability for webpages to successfully sniff user agents in the first place. Tor Browser and others uses this approach for improved privacy.

I can't resist wondering to what extent this cements the notion of Chrome and Edge having all of the browser market. Possibly not so much as my case is a very uncommon one. It's still interesting to think about.


 - [GNOME Web issues mentioning "user agent"](https://gitlab.gnome.org/GNOME/epiphany/-/issues/?search=User%20agent&sort=popularity&state=all&first_page_size=100)
 - [MDN on User Agents](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent)
 - [Tor blog post on fingerprinting and user agents](https://blog.torproject.org/browser-fingerprinting-introduction-and-challenges-ahead/)
