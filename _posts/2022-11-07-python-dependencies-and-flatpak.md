--
layout: post
title: Python Dependencies and Flatpak
description: How do you use Python dependencies in Flatpak?
tags:
  - linuxonmobile
  - code
---
I'm learning how to create responsive Gnome applications with Python, GTK4, and Flatpak. One of the early issues I ran into after I generated a new Python project using [Gnome Builder](https://flathub.org/apps/details/org.gnome.Builder)'s built in template was how to make Python dependencies from the Python package index aviable to my app.

I'm currently lacking a good resource describing the solution for my development log, so here is my take.

## Solution

If you generated your project using Gnome Builder, you likley have a JSON file in the root of your project directory it bears the name of your application identifier. This file, it turns out, is called a [Flatpak mainfest](https://docs.flatpak.org/en/latest/manifests.html).

It contains a section called "modules" which in my case is an array containing a single object(module for the application itself). This array, however, does not only take objects. It also takes strings/paths to other manifests. 

For each of one's PIP dependecies we need a module definations. Once generated, module sections might remind you of lock-files. It would be cubersome to create these "manually" or induvidually. So there is a "[Flatpak PIP Generator](https://github.com/flatpak/flatpak-builder-tools/tree/master/pip)" script that among, other things, that can generate these module definations given a `requirements.txt` file.

Put the `flatpak-pip-generator` script in the root of your project(you might want to add it to your `.gitignore`). Then create a `requirements.txt` file containing all your direct dependecies and then run:

```bash
./flatpak-pip-generator -r requirements.txt -o python-deps
```

The above should have generated a Flatpak manifest file named `python-deps.json` in the root of your project, containing one module defination for each dependency.

In the "modules" section in the initial Flatpak maifest one can then add a new entry `python-deps.json`. Now your app should build and run with all the dependecies avaible. If it dosn't run make sure you clean and rebuild the project as the module configs might be cached.

## Final notes

Here are some of the resources that I used while tinkering with the above: [Flatpak documentation](https://docs.flatpak.org/en/latest/python.html), a [StackOverflow question](https://stackoverflow.com/questions/58336157/using-gnome-builder-with-python) and a [Gnome Discourse question](https://discourse.gnome.org/t/gnome-builder-python-how-can-i-import-python-packages/6420).
