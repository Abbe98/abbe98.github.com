---
layout: post
title: Building Snowman sites on Github Actions
description: Examples of how to build Snowman sites on Github Actions with a little help from Oxigraphs' SPARQL server.
tags:
  - snowman
  - sparql
---

[Snowman][1] is a static site generator for SPARQL backends. HTML templates and SPARQL queries in, a website out.

I have a set of Snowman sites that needs to be built and deployed once a day to ensure that they are up to date. I wanted to do this a while back for one of them using Github actions.

The following Github action will:

1. Checkout the repository
2. Download the Snowman binary and make it executable
3. Run the Snowman `build` command

```yaml
name: build-and-deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    env:
      SNOWMAN_BINARY: https://github.com/glaciers-in-archives/snowman/releases/download/0.5.0/snowman-linux-amd64
    steps:
      - uses: actions/checkout@v3
      - name: Download Snowman
        run: wget "${{env.SNOWMAN_BINARY}}" -O snowman && chmod +x snowman
      - name: Run SPARQL server and build site
        run: ./snowman build
        # additional steps for deploying the contents of "site" directory
```

That's it, now you would have additional steps for deploying the contents of the `site` directory for the host of your choice.

Well, if you like me like having small sites that hold their data in one or a set of RDF files you won't have a SPARQL endpoint to query. The solution? Run the [Oxigraph][3] database in the same Github action!

In addition to the above the following Github action will:

1. Download the Oxigraph binary and make it executable
2. Load the RDF data into the Oxigraph database
3. Run Oxigraph and wait for it to start before running Snowman

```yaml
name: build-and-deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    env:
      OXIGRAPH_BINARY: https://github.com/oxigraph/oxigraph/releases/download/v0.3.16/oxigraph_server_v0.3.16_x86_64_linux_gnu
      SNOWMAN_BINARY: https://github.com/glaciers-in-archives/snowman/releases/download/0.5.0/snowman-linux-amd64
    steps:
      - uses: actions/checkout@v3
      - name: Download Oxigraph
        run: wget "${{env.OXIGRAPH_BINARY}}" -O oxigraph && chmod +x oxigraph
      - name: Download Snowman
        run: wget "${{env.SNOWMAN_BINARY}}" -O snowman && chmod +x snowman
      - name: Load RDF 
        run: ./oxigraph load --file static/data.ttl --location datastore
      - name: Run SPARQL server and build site
        run: ./oxigraph serve --location datastore & sleep 4 && ./snowman build
```

The `sleep 4` is there to give Oxigraph some time to start before running Snowman. It's not a very elegant solution and it would be awesome if someone(i.e. me) could make a [service container][2] for Oxigraph.

Still looking for a full real-world example? Check out the [Github action used to deploy FornPunkts Open Data site from a single DCAT RDF file][4].

[1]: https://github.com/glaciers-in-archives/snowman
[2]: https://docs.github.com/en/actions/using-containerized-services/about-service-containers
[3]: https://github.com/oxigraph/oxigraph
[4]: https://github.com/fornpunkt/open-data/blob/main/.github/workflows/build-and-deploy.yaml