---
layout: post
title: An Actionable Approach to Data Quality for Cultural Heritage Institutions
description: In this post I'm introducing a new data quality portal that we are currently testing with the K-samsöks data partners.
image: https://byabbe.se/assets/soch-data-portal-main.png
---
In this post I'm introducing a new data quality portal that we are currently testing with the K-samsöks data partners. It's a data quality tool without any percentages or metrics.

To solve data quality issues at cultural heritage institutions (or anywhere) two key things need to be achieved:

1. Awareness - individuals need to be aware of the specific data quality issues present in their data.
2. Actionability - individuals need to have the tooling and knowledge to find individual and fix quality issues.

The first one is something that aggregation actors have been targeting for a while through spreadsheets and percentages. The screenshot below shows the second(ish) iteration of our licensing statistics/issues spreadsheet that we share with data partners (the code behind it is written by my colleague Marcus and [it's open source](https://github.com/riksantikvarieambetet/soch-license-stats)).

![Sceenshot of spreadsheet containing SOCH license statitics](https://byabbe.se/assets/soch-license-stats.png)

Some institutions have been able to act upon the insights given by this, while others have not. A common issue is the lack of being able to query their own data, often this is because of lacking capabilities of collection management systems, sometimes it's a combination of this and user knowledge. No matter what it's a barrier.

Being an aggregator allows us to lower barriers for 70+ data partners so by curating and building a GUI around advanced queries. So instead of not being able to query their data or being stuck in writing some boolean and/or whatever query in their CMS they can now list problematic objects within a few clicks.

![Screenshot of the main SOCH data portal showing possible queries](https://byabbe.se/assets/soch-data-portal-main.png)

The current data quality queries available to data partners in the current proof of concept version of the data portal (we and partners have plenty of other ones in mind).

![Screenshot of an quality page displaying items with errors in a table.](https://byabbe.se/assets/soch-data-portal-main.png)

Following the selection of quality query and providing institution a list of problematic or possible problematic objects are presented to the user in a list containing a link back to the source page or CMS as well as other metadata that might be relevant for the given query.

In a couple of weeks it will be clear if this new approach have an impact. I know what I'm betting on.
