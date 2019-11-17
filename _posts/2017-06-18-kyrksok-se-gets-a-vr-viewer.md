---
layout: post
title: Kyrksok.se gets a VR Viewer
description: Last week I took the opportunity to add a VR Viewer for 360 degrees photos to the Kyrksok.se.
image: https://byabbe.se/assets/kyrksok.png
tags:
  - web technologies
---

![The Kyrksok logo](https://byabbe.se/assets/kyrksok.png)

Kyrksok.se is a directory for churches in Sweden that was [originally created last autumn over a weekend](https://byabbe.se/2016/11/12/kyrksok-se-and-wikidata). Last week I took the opportunity to add a VR Viewer for 360 degrees photos to the site.

It's primarily built on top of three.js and [WebVR-UI](https://github.com/googlevr/webvr-ui) and you can try it out [here](https://kyrksok.se/vr.html?q=10713923).

It's using the [WebVR API](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API) behind the scenes if you have a headset or Cardboard if not there is a fall-back for mouse and mobile devices.

One thing I would like to do with WebVR in the future is to play around with Mozillas [A-Frame](https://aframe.io/docs/0.5.0/introduction/) library together with OpenStreetMap 3D data, but for now I'm awaiting someone to put a VR-headset in my mailbox \:-)
