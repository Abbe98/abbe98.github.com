---
layout: post
title: MediaWiki development with SQLite and PHP
description: You don't need Vagrant, Docker, or any other set of fancy tools to hack on MediaWiki.
tags:
  - mediawiki
  - wikimedia
---
Recently I have been ranting a little bit about the many different solutions for setting up MediaWiki development environments. A visit to [mediawiki.org][1] and you will likely find solutions based on Docker, Vagrant, and custom CLI tools. Some are maintained, some are usable on some particular Linux distros, etc.

However, all you need for the vast majority of MediaWiki development is PHP and SQLite.

MediaWiki has limited SQLite support according to mediawiki.org, but I have found that it works for the vast majority of cases, and [incompabilities are tracked on Phabricator][2].

On Fedora, I get all the requirements for running MediaWiki with `dnf install php php-pdo`. Then I run `php -S localhost:8080` in the root of the MediaWiki repository and I'm good to go.

A downside is that I need to setup OpenSearch or Elasticsearch once in a while for tasks requiring CirrusSearch but that is a price I'm happy to pay for a stable and lightweight development environment.

[1]: https://www.mediawiki.org/wiki/MediaWiki
[2]: https://phabricator.wikimedia.org/tag/sqlite/
