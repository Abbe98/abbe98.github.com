---
layout: post
title: Github Pages with Cloudflare for SSL support
description: How I added SSL support to my Github Pages site by using Cloudflare.
image: https://upload.wikimedia.org/wikipedia/commons/9/9e/Cloudflare-logo-horizontal.svg
redirect_from:
  - /blog/2017/03/31/github-pages-with-cloudflare-for-ssl-support
---
One of the downsides with hosting this site on Github Pages has always been the lack of SSL support. From a SEO perspective it's supposed to be important(I have no clue), it's not a major thing for me people usually do not end up here after a Google search.

The main downside is that there is a bunch of cool (not so)modern web APIs such as Service Workers and Geo-location which does not work on insecure connections.

Cloudflare acts as a service between the users and the actual server, serving static content. This approach is perfect for Github Pages. This way content served through Cloudflare can be given a SSL certificate without the need for one between Github Pages and Cloudflare. This setup comes with a downside in the form of cache, because Cloudflare caches all content we do need to purge the cache when we make any changes to our site(such as this post). Github webhooks and the Cloudflare API is your friends.

Expecting a tutorial here? There is no need for one, I have never seen a better on boarding at any DNS provider. Create an account and enter you custom domain name, your DN-records will be imported and you will be assigned two name servers. Just a minor note, in the SSL settings you should select the "full" option and not the "flexible" one.

Now for even cooler demos \:-)
