---
layout: post
title: Cloning and Initializing Git Repositories for Work Tree Workflows
description: Two Fish shell function to make cloning and initializing Git repositories easy for work tree workflows.
image: https://byabbe.se/assets/git-work-tree-directory-structure.png
tags:
  - git
  - fish
  - tips
---

I'm very fond of Git work trees, but I'm rather opinionated regarding the directory structure of my projects. I prefer a "root" project directory containing my `.git` and all my work trees next to it. Like this:

```
my-project
  .git
  main
  feature-branch-1
  bug-branch-398
```

To accomplish the above with `git clone` you need to go through a few steps:

1. make a bare clone into given both the Git URI and the directory you want to clone it into
2. lookup the name of the default branch
3. add the work tree of said branch

That might not be a lot of work, but I care quite a lot about reducing friction, so I turned the above into a Fish shell function.

```fish
function git_clone_work_tree -d "make a bare clone of the given repository and creates a work tree for the default branch"
    set repository_url $argv[1]
    set repository_name $(basename $repository_url .git)
    git clone --bare $repository_url $repository_name/.git
    cd $repository_name
    set default_branch $(git remote show $(git remote) | awk '/HEAD branch/ {print $NF}')
    git worktree add $default_branch
end
```

It's as simple as:

```
git_clone_work_tree https://github.com/glaciers-in-archives/snowman.git
```

Which results in a directory structure:

```
snowman
  .git
  main
```

The same friction occurs when I need to turn a simple directory of files into a Git repository following the same directory convention. The following function moves the project initiates a bare repository adds a **new** work tree and moves all the project files there:

```fish
function git_init_work_tree -d "move the current directory to a child directory and make it the default branch in a new repository"
    set reopository_name $(basename $(pwd))
    set default_branch $(git config --get init.defaultBranch)
    git init --bare .git
    git worktree add --orphan $default_branch
    mv (ls -A | grep -v '^\.git$\|^'"$default_branch"'$') $default_branch/
end
```

These two shell functions make it much easier for me to accomplish a "Git work tree first" workflow as they are as easy as the initial Git commands and ensure Git work tree usage down the line does not pollute my parent directories.
