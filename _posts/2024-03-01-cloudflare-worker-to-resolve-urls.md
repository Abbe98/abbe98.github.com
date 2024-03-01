---
layout: post
title: Cloudflare Worker to resolve URLs
description: A Clouflare worker to resolve URLs and some edge cases.
tags:
  - cloudflare-workers
  - wikimedia
---

The other day, I needed to resolve a w.wiki URL from a client-side application. However, the UrlShortener MediaWiki extension does not provide an API for resolving URIs ([T358049](https://phabricator.wikimedia.org/T358049)), and client-side applications can't simply resolve the URLs normally due to CORS.

To unblock myself, I decided to write a generic Cloudflare Worker to resolve URLs, as it is a common task and I always end up dealing with the same edge cases, such as content negotiation and URL fragments. I will update the code below as I need to handle more cases.

```javascript
// Created by Albin Larsson and made available under Creative Commons Zero
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});

async function handleRequest(request) {
  const urlParam = new URL(request.url).searchParams.get('url');

  if (!urlParam) {
    return new Response('URL parameter is missing.', { status: 400 });
  }

  const corsHeaders = {
    'Access-Control-Allow-Origin': '*',
    'Access-Control-Allow-Methods': 'GET, HEAD, OPTIONS',
  };

  // manually follow redirects to obtain the final URL from the location header
  // as the client-side only fragment wont be a part of the URL-object
  let finalUrl = urlParam;
  let response;

  do {
    // pretent to be human by requesting text/html to prevent default content-neogtiation
    response = await fetch(finalUrl, { redirect: 'manual', headers: { 'Accept': 'text/html' } });

    if (response.status >= 300 && response.status < 400) {
      const redirectUrl = new URL(response.headers.get('location'), finalUrl);
      finalUrl = redirectUrl.href;
    }
  } while (response.status >= 300 && response.status < 400);

  return new Response(finalUrl, {
    headers: {
      ...corsHeaders
    }
  });
}
```