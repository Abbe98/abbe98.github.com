---
layout: post
title: My Self-hosting Setup
description: I'm sharing what services I self-host and what hardware it's using.
tags:
  - tips
---

Having self-hosted various tools and services for a few years, I now believe I got a solid home server setup that covers almost all of my use-cases, and therefore I thought I would share my current setup.

### Core services

[Pi-hole](https://pi-hole.net/)

While the common use case for Pi-hole is content and ad-blocking I use it as both a DNS and DHCP Server in addition to content blocking. It essentially keeps most of my network management in one place. Pi-hole is a must-have piece of software for me nowadays as it makes browsing faster and saves a lot of battery for all of my devices.

[Apache/WebDav](http://httpd.apache.org/docs/current/mod/mod_dav.html)

Apache and in particular its [WebDav](https://en.wikipedia.org/wiki/WebDAV) module is what I use for file sharing and synchronization. WebDav might be an old and scray protocol, but its ecosystem is great. WebDav just works with all kinds of clients most importantly for me with [Nemo](https://github.com/linuxmint/nemo)(file manager) and [Joplin](https://joplinapp.org/)(note-taking).

[Rclone](https://rclone.org/)

I use Rclone to make backups of my WebDav enabled files as well as some other services.

[Jellyfin](https://jellyfin.org/)

I used to self-host [Calibre-web](https://github.com/janeczku/calibre-web) for my eBooks, but after a couple of pull requests to the Jellyfin user interface, I now use it as a more general-purpose system. Today I use it to host eBooks, photographs, radio shows, and papers. 

In addition to the services above I also host a few major technical tools like [JupyterHub](https://jupyter.org/hub), [Jena Fuseki](https://jena.apache.org/documentation/fuseki2/) / [Thor SPARQL editor](https://github.com/Abbe98/thor/projects), and [Git](https://git-scm.com/).

### Wishlist

Firefox sync

I don't use Mozilla's sync service but instead, I have a [backup script](https://byabbe.se/2020/09/16/my-essential-backup-script) to backup my bookmarks, history, etc. It would however be nice to have a live sync service for my own devices. The [open source service Mozilla provides](https://github.com/mozilla-services/syncserver) is however rather complex and nothing I feel like hosting at this point, especially as I don't have a current need for Docker.

### Hardware

Everything is hosted on a Raspberry Pi 3b+ that boots from an SSD. A second Raspberry Pi 3b+/SSD hosts Rclone and periodically makes backups of the main Pi's WebDav service.
