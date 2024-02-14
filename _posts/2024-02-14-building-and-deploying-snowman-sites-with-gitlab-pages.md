---
layout: post
title: Building and deploying Snowman sites with Gitlab Pages
description: How to build and deploy Snowman sites on Gitlab Pages, or just copy the `.gitlab-ci.yml` configuration template.
tags:
  - snowman
  - sparql
---

I have [previously written about how to build Snowman sites on Github Actions][1]. Yesterday I had to figure out not only how to build Snowman sites on Gitlab Pages but also how to deploy them. Not only was the Gitlab CI/CD configuration a joy compared to Github Actions, but it integrats well with the Gitlab Pages service to the extent that any Snowman site should be able to build and deploy with the following `.gitlab-ci.yml` configuration:

```yaml
# The Docker image that will be used to build your app
image: debian:bookworm
# Functions that should be executed before the build script is run
before_script:
  - apt-get update && apt-get install --yes ca-certificates && apt-get install --yes wget
  - wget
    "https://github.com/glaciers-in-archives/snowman/releases/download/0.5.0/snowman-linux-amd64"
    -O snowman && chmod +x snowman
pages:
  script:
    - ./snowman build
  publish: site
  artifacts:
    paths:
      # The folder that contains the files to be exposed at the Page URL
      - site

  rules:
    # This ensures that only pushes to the default branch will trigger
    # a pages deploy
    - if: $CI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
```

Now if you want to build it with local RDF files you would need to setup Oxigraph or another SPARQL service just like in the Github Actions example. I haven't needed that yet so I leave that exercise to the reader.

[1]: https://byabbe.se/2023/11/15/building-snowman-sites-on-github-actions
