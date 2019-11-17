---
layout: post
title: Enabling CORS in SOCH with a Proxy on Google App Engine
description: Adding CORS support to the SOCH API with a free proxy on Google App Engine
image: https://byabbe.se/assets/soch-logo.jpg
tags:
  - soch
---

**Update** SOCH now supports CORS.

One of my favorite APIs is SOCH also known as K-Sams&ouml;k, I love it because of it's content. In the time of writing it contains 6117658 heritage items. 

The API has several disadvantages too the biggest one is probably that it's "Linked Data First"(I might just invented that expression), the second one is licensing(it's messy and got some conflicts), the third one is that it does not support CORS(Cross-origin resource sharing) so you cant use it directly from a client.

Therefor I created a SOCH proxy for Google App Engine that enables CORS and supports all features of the API such as XSLT stylesheets and JSON-LD(through custom request header).

Thanks to Google App Engine it's totally free to host and run. The source is available in my [ksamsok-proxy-gae](https://github.com/Abbe98/ksamsok-proxy-gae/) repository at Github.

### Notes
 
 **XSLT stylesheets**

The XSLT stylesheets is served directly from within this app. The stylesheets used are the ones from the latest open sourced version of K-Sams&ouml;k. That version was released in 2013 so the ones this application serves might differ from the ones on K-Sams&ouml;ks servers. If you run into trouble please open a issue and I will look into it.

**JSON-LD**

K-Samsök supports JSON-LD through a custom HTTP header(Accept format), this is also available through this proxy. But in some rare cases it does not work, because all web browsers and web servers does not support HTTP headers with spacing. This issue exists with regular use of the K-Sams&ouml;k API too.