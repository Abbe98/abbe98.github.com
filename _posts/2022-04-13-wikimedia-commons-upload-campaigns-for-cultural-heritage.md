---
layout: post
title: Wikimedia Commons Upload Campaigns for Cultural Heritage
description: Together with Wikimedia Sverige I have created reusable upload campaigns for Wikimedia Commons focusing on cultural heritage.
tags:
  - fornpunkt
  - wikimedia
---
Since the first Swedish edition of Wiki Loves Monuments in 2011, participants have uploaded almost 30 000 images of heritage sites, protected buildings, ships, and working life museums.

Wiki Loves Monuments (WLM) goes on for 30 days per year. While many experienced users take images all year round for the event, many new contributors are introduced to WLM and the broader Wikimedia community for the first time through the 30-day event. What if there was a just as engaging effort for documenting heritage environments that would go on not for 30 days a year, but for 365?

Wiki Loves Monuments builds to an extent upon a Wikimedia Commons called [Campaigns](https://commons.wikimedia.org/wiki/Commons:Upload_campaigns). Campaigns make it possible to construct upload forms with a set of predefined values or have default values passed through Campaigns URLs.

Much of the Wiki Loves Monuments tooling (maps, lists, etc) uses WLM specific Campaigns to define values for things like the identifiers of monuments and sites. It's super easy to create these links:

```
https://commons.wikimedia.org/w/index.php?title=Special:UploadWizard&campaign=wlm-se-arbetsl&id=<museum-identifier>
```

However, it's not that easy to reuse these Campaigns for non-WLM usage. The help texts are WLM specific, they set WLM-specific categories, etc. Nor is it easy to create a new Campaign. You will need special user rights and experience with JSON and Wikitext.

So rather than to set up tool-specific Campaigns, what if we had generic ones that any tool could integrate without needing to worry about set up and help texts?

Such Campaigns now exist thanks to [Wikimedia Sverige's community support](https://se.wikimedia.org/wiki/St%C3%B6d_till_gemenskapen/Projektst%C3%B6d/Generella_Commons_Kampanjer_f%C3%B6r_kulturmilj%C3%B6er)! It doesn't matter if you want to crowdsource images from a spreadsheet or if you are a programmer wanting to integrate uploading into your tool or app. You can use these Campaigns.

 - [Heritage sites/Monuments](https://commons.wikimedia.org/wiki/Campaign:Kulturl%C3%A4mningar)
 - [Working Life Museums](https://commons.wikimedia.org/wiki/Campaign:Arbetslivsmuseum)
 - [Protected buildings](https://commons.wikimedia.org/wiki/Campaign:Byggnadsminnen)

Two tools already utilizing these Campaigns are [Kyrksök.se](https://kyrksok.se/map.html) (database of churches in Sweden) and [FornPunkt.se](https://fornpunkt.se/karta) (FornPunkt is a citizen-science platform for historic sites).

You can create upload links for these Campaigns similarly to how one does it for WLM:

```
https://commons.wikimedia.org/w/index.php?title=Special:UploadWizard&campaign=Kulturl%C3%A4mningar&id=<monument-identifier>
```

The 30 000 images contributed through Wiki Loves Monuments add to the tens of thousands of images uploaded by individual contributors and cultural heritage institutions. Today Wikimedia Commons has the largest public collection of images depicting Swedish heritage sites. Wikimedia Commons is, therefore, an important and open piece of infrastructure for cultural heritage in Sweden. It's utilized by various organizations,  including the [Swedish National Heritage Board and its website "Kringla"](https://www.k-blogg.se/2012/11/08/nu-har-vi-kopplat-ihop-kringla-och-wikipedia/) which indexes Wikimedia Commons once every week.

By creating these generic and easy-to-use Campaigns, the hope is to lower the barrier for integrations to contribute to this public collection of information. Your aim does not need to be to create the next Wiki Loves Monuments.
