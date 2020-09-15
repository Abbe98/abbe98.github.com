---
layout: post
title: The AWW Library
description: Intruduction to AWW a AJAX Library for minimal AJAX requests within WebWorkers.
tags:
  - code
---

I'm not a big fan of jQuery, but I do **many** AJAX calls. Most time I just write the AJAX calls straight into my code, it works fine! :-) Some days ago I did some work with [WebWorkers][1]([Get it, it's good stuff][2]), as in many of my tests I'm adding jQuery to do things just a bit faster(by that I mean my coding speed). I ran into the issue that I can't use jQuery in a WebWorker, and writing it the `XMLHttpRequest` way for all my future WebWorker tests? No thanks. 

You already know what I did next.

I do now that there is tons of small AJAX libraries in the wild, but not to many that's below two kb in size, works with WebWorkers and most important made by me ;-)

### AWW
*Minimal AJAX requests for WebWorker usage.*

 - <2kb compressed 
 - IE 7+
 - Can't be more simple
 - Made by some weird human :-)
 - Open source

Say hello to `AWW.ajax()`, `AWW.get()` and `AWW.post()`.

Simple example:

<pre class="line-numbers"><code class="language-javascript">AWW.ajax({
  url: "http://filltext.com/?rows=10&business={business}&location={city}&pretty=true",
  success: function(data) {
    document.getElementById('results').innerHTML = data;
  }
});
</code></pre>

WebWorker example:

<pre class="line-numbers"><code class="language-javascript">importScripts('../../aww.js');

getData();
setInterval(getData, 1000);

function getData() {
  AWW.ajax({
    url: "http://filltext.com/?rows=10&business={business}&location={city}&pretty=true",
    success: function(data) {
      postMessage(data);
    }
  });
}
</code></pre>


For the full working examples see the ["tests"][3](**NOTE:** You will need a web server to run the WebWorker example).

It's very easy to learn just [by reading the code][5].

If you would like to explore AWW a bit deeper check it out on [Github][4].

[1]: https://developer.mozilla.org/en-US/docs/Web/Guide/Performance/Using_web_workers
[2]: http://www.html5rocks.com/en/tutorials/workers/basics/
[3]: https://github.com/Abbe98/AWW/tree/master/tests
[4]: https://github.com/Abbe98/AWW
[5]: https://github.com/Abbe98/AWW/blob/master/aww.js