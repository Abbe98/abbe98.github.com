---
layout: post
title: Partial updates of large Snowman sites
description: How can you make partial updates of large Snowman sites?
tags:
  - snowman
  - sparql
  - govdirectory
---
[Snowman][1] is a static site generator for SPARQL backends, since its inception a goal has been that one should be able to use it to build large sites with 100,000 pages. Oneway Snowman makes this possible by relying heavily on the caching of all SPARQL queries.

Building the [Govdirectory][2] website from a blank cache would issue thousands of SPARQL queries to the Wikidata Query Service. This, however, rarely happens since Snowman's built-in cache "manager" allows one to selectively invalidate parts of the cache. Let's see how one would use this feature to update parts of the Govdirectory website.

### Basic real-world examples

**Remove all top-level country data**

```bash
snowman cache countries.rq --invalidate
```

The above invalidates the cache for the `countries.rq` query.

**Remove all account data for Icelands Ministry for Foreign Affairs**

```bash
snowman cache account-data.rq Q15983772 --invalidate
```

The above invalidates the cache for the instance of the `account-data.rq` query which was called with `Q15983772` as its only argument.

### An advanced real-world example

Now, what if you want to update all account data for all Icelandic government agencies? Because the `account-data.rq` is no different between countries you can't only rely only on Snowman's cache invalidation. Instead, we need to involve some scripting.

**Update all account data for all Icelandic government agencies**
```bash
#/bin/sh

for i in $(find site/iceland/* -type d);
  do
  qid=$(echo ${i%%/} | cut -f3 -d"/");
  echo $qid
  snowman cache account-data.rq $qid --invalidate
done
```

The above script takes advantage of the fact that Govdirectory uses the identifiers from Wikidata to both build its output URIs and parameterize its SPARQL queries. The script iterates over all directories in the `site/iceland/` directory(`site` being the directory to which Snowman writes its output) and extracts the Wikidata identifier from the directory names. It then invalidates the cache for the `account-data.rq` query for each of the directories.

### Conclusion

Behind the scenes Snowman's cache manager will first hash the query file name and subsequently the *issued* query. Thus, a hierarchy of directories is created where the first level is the hash of the query file name and the second level is the hash of the *issued* query. This is what enables Snowman's support for selectively invalidating the cache.

In the cache Snowman stores the raw SPARQL resultsets in JSON and the `cache` command allows one to inspect the cache. For example, to see the cache for the `account-data.rq` query for the Icelandic Ministry for Foreign Affairs one would run:

```bash
snowman cache account-data.rq Q15983772
```

When planning to build a large site with Snowman I would recommend that you first put time into thinking how easy your information/data model is to query. That can be tricky with a project utilising open models such as the one of Wikidata and Wikibase, but Snowman 

Do you have suggestions for how Snowman could improve its support for large sites? Check out the dedicated **[large-project-support][3]** issue tag on Github!

[1]: https://github.com/glaciers-in-archives/snowman
[2]: https://govdirectory.org
[3]: https://github.com/glaciers-in-archives/snowman/issues?q=is%3Aissue+is%3Aopen+label%3Alarge-project-support
