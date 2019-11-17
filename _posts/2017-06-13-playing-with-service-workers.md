---
layout: post
title: Playing with Service Workers
description: I recently played around with Service Workers to learn.
image: https://byabbe.se/assets/default.png
tags:
  - web technologies
  - code
---
I'm on a learning spree targeting web technologies, recently I played around with [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) adding functionality to some of my existing projects.

One of the projects I enchanted with offline support was my "[bookshelf](https://byabbe.se/books/)" a web app for browsing and searching the books I own. It's a simple static site reading the contents from a single JSON file witch I update every now and then.

Two prerequisites that I had was\:

 - I compared everything to [AppCache](https://developer.mozilla.org/en-US/docs/Web/HTML/Using_the_application_cache).
 -  I used Opera for development.

### AppCache

Back an few years ago when AppCache was a new piece of the web, my and others approach to offline web apps was primarily simple, all files to be cached was defined in a manifest, all files only available over network and files for fallback was defined in the same file. When ever dynamic data was needed to be dealt with storing its content in LocalStorage or IndexedDB was an obvious approach. A update to the cache was triggered by changing something in the manifest(such as a comment).

```
CACHE MANIFEST
# 0.0.1
# comment
index.html
another-page.html
style.css
image.png

NETWORK:
network.html

FALLBACK:
fallback.html
```

It was possible to give a very basic site offline support in 30 seconds, but for anything with dynamic content you needed a strategy for storing and updating data.

### Opera

Honestly I never got Opera to work with local development and Service Workers, I did a bunch of research into the topic of Chromium and the need of using `localhost`(not `127.0.0.1`) for development etc. Official examples could just do noting without any visible errors and I newer made sense of the random(at least for me random) network errors that sometimes showed up.

Switching to Firefox made everything work, out of the box, but it took me a while to do so.

### My First Project

So going back to my bookshelf, my requirements for offline support was very basic, I wanted the cache to be automatically updated whenever network was available, I wanted all cache related code to be contained within the service worker, and not in the UI/main thread.

<pre><code class="language-javascript">const CACHE_NAME = 'abbesbooks';

self.addEventListener('install', e => {
  e.waitUntil(
    caches.open(CACHE_NAME).then(cache => {
      return cache.addAll([
        '',
        'index.html',
        'style.css',
        'list.min.js',
        'app.js',
        'books.json'
      ]);
    })
  );
});

self.addEventListener('fetch', event => {
    event.respondWith(loadFromCache(event.request));
    event.waitUntil(updateCache(event.request));
});

function loadFromCache(request) {
  return caches.open(CACHE_NAME).then(cache => {
    return cache.match(request).then(match => {
      return match || Promise.reject('failed-match');
    });
  });
}

function updateCache(request) {
  return caches.open(CACHE_NAME).then(cache => {
    return fetch(request).then(response => {
      return cache.put(request, response);
    });
  });
}</code></pre>

The Service Worker above is everything I did(except registering the Service Worker). At first I found thing like `waitUntil()` a bit weird but it made sense when I thought about JavaScript in general, although nothing like it seams to be required in Web Workers. 

It should be noted that the example above is not a very useful example in most real world examples as it saves the user no data and displays old data until the page is refreshed once. It works for my needs but `updateCache()` could be limited to `books.json` and the view updated when fetched over the network.

AppCache gave us no control over the cache through JavaScript, Service Workers and the Cache API does just that and we can deal with dynamic contend without the need of other storage solutions.

I'm looking forward to play more with Service Workers especially in a non-cache context like load-balancing and Push notifications.
