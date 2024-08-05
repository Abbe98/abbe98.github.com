---
layout: post
title: Reconcile Against any MediaWiki Instance
description: We created a reconciliation service supporting any MediaWiki and Wikibase instances for others to use in OpenRefine.
image: 
tags:
  - wikimedia
  - wikidata
  - openrefine
  - wikibase
---
You have just deployed your 55th [reconciliation service](https://www.w3.org/community/reports/reconciliation/CG-FINAL-specs-0.2-20230410/) for a MediaWiki or Wikibase-based service. You start wondering if this isn't the time to stop copy-pasting your code around and apply some of that don't-repeat-yourself wisdom. That was me a moment ago after a few months of pushing it in front of me. Now a prototype intended to replace all of our reconciliation services targeting MediaWiki and Wikibase is here and you can give it a go in OpenRefine!

Let's jump in head first with some example endpoints:

```plaintext
https://kartkod.se/apis/reconciliation/mw/en.wikipedia.org/ # English Wikipedia (MediaWiki)
https://kartkod.se/apis/reconciliation/wb/wikibase.world/ # Wikibase World (Wikibase)
https://kartkod.se/apis/reconciliation/wb/www.wikidata.org/ # Wikidata (Wikibase)
https://kartkod.se/apis/reconciliation/mw/www.wikidata.org/ # Wikidata (MediaWiki)
https://kartkod.se/apis/reconciliation/mw/en.wikisource.org/ # English Wikisource (MediaWiki)
# your wiki? and many more!
```

You see the patterns, now let's see how we got here. Once you realize you can put any domain in there, you might think that we made it very error-prone and complex. We did, here is why:

**It's not error-prone to us**

You see, our OpenRefine users can't add their own reconciliation services and our collection of services is already there the first time they sign in.

**We want it to be open to you**

If we needed to allow-list all the configurations it would quickly become less useful to others and we need it to hook into our other reconciliation services with local restrictions anyway. It's an experiment and I hope we can keep it configuration less.

**We need it to be stateless**

We deploy all our reconciliation services in a distributed way and keeping our services stateless is incredibly useful to limit the maintenance and engineering needed.

### Future work

This service is experimental and you should expect it to change in the coming weeks as we bring it on pair with our existing services. It will never implement the whole Reconciliation specification but

 - Wikibase reconciliation beyond items(properties are especially important)
 - Documentation on how to reconcile against specific namespaces
 - Documentation on how to reconcile against Wikibase items with certain statements
 - Error messages and service validation(things that aren't MediaWikis, things without necessary extensions, etc)
 - Auto generation of usage documentation based on installed extensions(CirrusSearch, etc)
 - Support Wikimedia Commons entities(it's a weird one and given the state of Structured Data on Commons it's not highly prioritized)

**A note on compatibility with the OpenRefine Wikibase extension**, our reconciliation services consider the Wikibase URIs as the "true" identifiers while the Wikibase extension expects just the QID. Hopefully, this is something I can work on upstream as it's not an option to change the behavior on our end. In the meantime you might be able to work around this using the "Use values as identifiers" feature.

I hope you give it a try, if you have any questions or suggestions feel free to reach out. I will also be at Wikimania if you want to chat in person!
