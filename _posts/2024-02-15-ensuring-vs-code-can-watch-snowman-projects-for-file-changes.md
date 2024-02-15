---
layout: post
title: Ensuring VS Code can watch Snowman projects for file changes
description: Fixing the "Visual Studio Code is unable to watch for file changes in this large workspace" error when working with Snowman projects.
tags:
  - snowman
---

Rencently VS Code and VS Codium has been throwing the following error at me when working with Snowman projects:

> Visual Studio Code is unable to watch for file changes in this large workspace

Turns out that VS Code is trying to watch all the files in the `.snowman` directory and it's subdirectories. No wonder it's complaining, there are a lot of files in there!


Adding `.snowman` to the `files.watcherExclude` setting in the VS Code settings solved the issue accross all my Snowman workspaces.

Now if do want to watch the `.snowman` directory for changes one thing you can do is to try to reduce the number of files in there by deleting old cache data with the following Snowman command:

```bash
snomwan cache --invalidate
```

This can be good practice to do anyway every now and then to keep folder from growing larger and larger.
