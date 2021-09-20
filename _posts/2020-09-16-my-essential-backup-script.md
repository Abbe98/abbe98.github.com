---
layout: post
title: My Essential Backup Script
description: In this blog post, I show my personal backup script that I use regularly.
tags:
  - tips
---
On my main computer, there are essentially three things that change regularly and aren't backed up to a could service regularly. These three things are notes, browser bookmarks, and keys/passwords. To be able to back up these to external servers without the hassle, I wrote a Bash script a while back that allows me to type `backup` anywhere in my terminals to quickly get an encrypted zip containing these files.

The following code can be placed in a file named `backup` inside of `/usr/bin` and once you have made sure your everyday user is set as the owner you are good-to-go. Typing `backup` should prompt you for an encryption key and following that you should have two backup files in your current directory. You should of course change the file paths as needed for you, the example is for my use of Joplin, Firefox, and Seahorse.

### Some Final Notes

 - Don't name the file "backup" (I haven't) give it a name only you know.
 - It's not using zip's built-in encryption [nor should anyone](https://en.wikipedia.org/wiki/Zip_(file_format)#Encryption).

<pre><code class="language-bash">#!/bin/bash

echo "Starting backup"

echo "Locating Firefox profile."

FIREFOX_PROFILE=$(find ~/.mozilla/firefox/ -maxdepth 1 -type d -name *.default | head -1)

echo "Firefox profile found at: ${FIREFOX_PROFILE}"

SSH="${HOME}/.ssh"
KEYS="${HOME}/.local/share/keyrings"
BOOKMARKS="${FIREFOX_PROFILE}/places.sqlite"
NOTES="${HOME}/.config/joplin-desktop"

echo "Directories selected for backup:\n${BOOKMARKS}\n${KEYS}\n${SSH}\n${NOTES}"

echo "Zipping directories"
zip -r backupoutput.zip ${BOOKMARKS} ${KEYS} ${SSH} ${NOTES}

echo "Encrypting zip file"
gpg -c backupoutput.zip

echo "Done, remember to delete both files"
</code></pre>