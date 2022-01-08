---
layout: post
title: Notes on launching an MVP
description: Following a decade of procrastination, I decided that it was about time to create a Swedish citizen-science platform for heritage sites and historic environments. Here are my notes from the launch.
image: https://byabbe.se/assets/fornpunkt.png
tags:
tags:
  - crowdsourcing
  - fornpunkt
---
Following a decade of procrastination, I decided that it was about time to create a Swedish citizen-science platform for heritage sites and historic environments and 80 work hours later I launched [fornpunkt.se](https://fornpunkt.se/).

I have built quite a few crowdsourcing platforms [some over a long period of time](https://byabbe.se/2015/10/25/biocaching-continues), [some over a very short period of time](https://byabbe.se/2015/01/07/holiday-project-ksamsok). However, I'm not sure any of them would qualify as even close to a **minimum** viable product at their launch. FornPunkt was however, rather close to minimal while still functional.

## The functionality of the MVP

 - **Content editing** Users could give a site a simple geometry, write a textual description and add a class. Users could edit and delete these sites.
 - **Discovery and browsing** Users could browse user-created sites on a map as well as sites from the government-run register "The Archaeological Sites and Monuments System"(KMR). Users can comment on both sites created by other users and ones from KMR. Users could add custom background maps (WMS/XYZ-services, etc) as backgrounds.
 - **Export** Users could export their data.
 - **Documentation** Documentation wise there were only some docs about using advanced map features.

## Reasons for the MVP approach

**Motivation** Seeing early users register hundreds of sites is way better than ticking a box.

**Not painting yourself into a corner** Two days into the MVP I realized from watching users that using the Swedish National Heritage Board's classification wasn't good enough for my type of user. If I would have spent another 80 hours on it, I would have integrated more with this classification. Now I started decoupling from it a week after launch.

**Real-world usage** Real-world usage gives you indications not only regarding usage and features but also regarding technical bottlenecks.

## Things that worked well

**Waiting list/invite** FornPunkt is at this early stage invite-only, not only does this allow me to connect with users but it also gives me a reason to ask how they would like to use it. The largest group are researchers wanting to store sites and data they collect. The second-largest group is all professionals, mostly from government agencies. Great, advanced users, let's cover their needs early on. Also, the invite-only approach allows me to leave investment into moderation features to the future me.

**The feature set** Structured data is great, but if an option for a particular type of information does not exist, users will happily enter the data into a free-text field. That's great as one can look at the free text and see which structured data fields should be prioritized. Advanced map features and export might not be obvious in the MVP but these helped to attract interest and stand out from existing services.

**The infrastructure** I launched the servers and databases the day before the launch, and other than a CSS file not being purged on an edge-server correctly, everything worked perfectly. Managed services are great, and I should maybe have used more proprietary services infrastructure. If you spend little time on something, the risks of lockin are rather low.

**Stakeholder revelations** I didn't think much of stakeholders regarding the data and side services of FornPunkt. Since launch five companies and four government agencies have expressed interest in exchanging data and two pilots are being prepared.

## Things that worked less well

**Onboarding** Interfaces are scary, especially ones where you can edit public data. Combining that with a lack of introductory documentation there was clearly a barrier to the first contribution. Considering how easy it is to make a screencast and demo today, I should have done it from the start, for the next MVP I will.

**Transparency** A site footer didn't make it into the MVP, until two hours after launch. An about page? No that didn't make it either until two hours after launch which was needed to explain that it was an early stage MVP. I played catchup all launch week with transparency and things like a public changelog and an overview of future work.

**Invitation management** I have enterprise-grade systems for automatic tests, automatic deployment, automatic error management, etc. All to save me time but for the invite system, I went with a spreadsheet and list of invite codes managed by me copy-pasting. Which invite codes had been shared? Which ones have been used for who? It wasted so much time and focus that I could have spent on talking to users, fixing bugs, and laying on the sofa. Never again.

## Final notes

Tech is easy understanding problems are hard. Several features that felt prioritized at the start are no longer planned. New features that three weeks of usage could unravel while a decade of procrastination couldn't are now planed. Launching early has probably saved me the 80 hours I spent on the original MVP.