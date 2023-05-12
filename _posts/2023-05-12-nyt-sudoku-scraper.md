---
layout: post
title: New York Times Sudoku Scraper
description: A Python script for scraping the New York Times' daily sudoku puzzle.
tags:
  - python
  - tips
---
You get home late and go to bed only to find that you missed the New York Times' daily sudoku puzzle? Maybe you skip the puzzle one day? Or maybe you just want to play it in an app of your choise.

I just wrote a basic script, which uses Regular Expressions to extract the puzzle from the New York Times website. I'm particularly fond of how it parses the JavaScript game data as JSON, who knows how long it will last. Combined with a sheduled Github Action's workflow and a little bit of [Git scraping](https://simonwillison.net/2020/Oct/9/git-scraping/) it should pull the hard pussle each day and store it in a [.sdk file](http://sudocue.net/fileformats.php).

The script is available on [Github](https://github.com/Abbe98/nyt-sudoku-scraper) and hopefully it will build up a nice Sudoku archive over time. Now I just need to make it easier to load custom games into [GNOME Sudoku](https://gitlab.gnome.org/GNOME/gnome-sudoku).
