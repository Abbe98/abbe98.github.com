---
layout: post
title: Revisiting a Project with Serverless
description: I'm revisiting an old project to experiment with serverless infrastructure.
image: https://byabbe.se/assets/default.png
tags:
  - runes
  - code
---

Two years back I [wrote about runor.rocks](https://byabbe.se/2018/12/19/a-five-minute-hack) a small service I built in five minutes that redirects you to a random article about a runestone. An issue with the solution was speed so when I wanted to explore Serverless a while back it was the perfect small project to revisit. 

The task at hand was very simple, given a set of URLs redirect to one of them randomly. Small task and perfect for experimenting with Serverless.

I went with [Cloudflare Workers](https://workers.cloudflare.com/) as the serverless option, mainly because I'm already a Cloudflare customer.

The first thing that impressed me was its Editor, I could code and test the entire service directly on the website, sure it's a very simple script but often the first barrier is the one that matters the most. Deploying isn't a thing saving the file and done, for a critical service I imagine you would need a local or staging environment but compared to the same for a VPS it's a breeze.

My script ended up looking like the following:

<pre><code class="language-javascript">addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
});

async function handleRequest(request) {
  const runes = [
    'https://en.wikipedia.org/wiki/S%C3%B6dermanland_Runic_Inscription_245',
    'https://en.wikipedia.org/wiki/Jelling_stones',
    'https://en.wikipedia.org/wiki/Kirkjub%C3%B8ur_stone',
    '...',
  ];

  const redirect = runes[Math.floor(Math.random() * runes.length)];

  return Response.redirect(redirect, 307);
}
</code></pre>

One thing I wanted to think about when I explored Serverless were the vendor lock-in, now after having this and two other of my hobby projects migrated to Cloudflare workers my concern is mostly migrated. If one uses it for small microservices that doesn't need heavy integration with storage I would consider it. I would however not use a similar service from a small business, startup, or Google because one's code just can't run anywhere in case they shutdown.

My overall impression is very good it eliminates many of the maintenance and deployment hurdles and the amount of lockin is okay for basic microservices in my opinion. In many projects, I would however consider them technical debt.

Since this experiment Cloudflare Workers has become even more inviting, things like [elimination of cold starts](https://blog.cloudflare.com/eliminating-cold-starts-with-cloudflare-workers/) and [Python support](https://github.com/cloudflare/python-worker-hello-world) will make it stay as my go-to option for serverless.
