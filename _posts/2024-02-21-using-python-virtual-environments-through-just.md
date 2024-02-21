---
layout: post
title: Using Python virtual environments through Just
description: How to setup your Justfile to use Python virtual environments through Just
tags:
  - django
  - python
---
I have gotten quite fond of Just lately much thanks to how it forces you into the habit of creating structured documentation for the various commands and scripts that you end up writing.

When adding a Justfile to a Python/Django project the other day I found myself in a situation where I wanted to make sure that all commands ran in a virtual environment. However, because Just run each line in a separate shell, it is not possible to activate the virtual environment in one line and then run the command in the next.

The only (sane) way I found to solve this was to prefix each command with the path to the virtual environment's Python or Pip binary. This is not ideal, but it's likley that you and your colaborators will have settled on a naming convention for the virtual environment directory anyway.

Here is a full example of a Justfile form one of my Django projects:

```
# load .env file
set dotenv-load

@_default:
  just --list

# setup virtual environment, install dependencies, and run migrations
setup:
  python3 -m venv .venv
  ./.venv/bin/pip install -r requirements.txt
  ./.venv/bin/python -Wa manage.py migrate

run:
  ./.venv/bin/python -Wa manage.py runserver

test:
  ./.venv/bin/python -Wa manage.py test

# virtual environment wrapper for manage.py
manage *COMMAND:
  ./.venv/bin/python manage.py {{COMMAND}}

```
