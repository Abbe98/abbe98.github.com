---
layout: post
title: Observations on AI Assisted Crowdsourcing
description: Observations on AI assisted crowdsourcing during a recent project together with museums in Sweden.
image: https://byabbe.se/assets/smv-description-translations.png
tags:
  - ai
  - crowdsourcing
  - wikimedia
---
As a part of the "[Wikimedia Commons Data Roundtripping](https://meta.wikimedia.org/wiki/Wikimedia_Commons_Data_Roundtripping)" project facilitated by me in my role at the Swedish National Heritage Board we ran a pilot together the Swedish Performing Arts Agency around crowdsourcing translations of image descriptions this spring. In this post I'm briefly sharing some of my observations related to how AI assisted translations impacted the crowdsourcing campaign.

So to begin what did we do? We uploaded 1200 images to Wikimedia Commons all with descriptions in Swedish. Then we invited people to translate those descriptions into English using a tool built for that specific purpose.

![screenshot of the user interface made for the crowdsourcing campaign](https://byabbe.se/assets/smv-description-translations.png)

In addition to the empty input field for the user to fill in there was also the "Google Translate" button. This button would prefill the input with the automatic translation from Google (the user would still need to edit/submit it). Except it was a little easier said then done...

Every now and then there would be an encoding error in the string returned from Google:

"Anna-Lisa Lindroth as Ofelia in the play Hamlet, Knut Lindroth​**\&#39;**​s companion 1906. Scanned glass negative"

This type of errors were discovered during development of the tool but we decided to leave the issue there to see if users would catch it.

A while into the crowdsourcing campaign it became clear that the descriptions translated by Google Translate were of higher quality then the ones done entirely by humans. While it didn't manage all the theater specific terms it was still simply more consistent.

After an user had been using the Google Translate button for a while without many or any edits needed they no longer caught obvious error such as the example above. The pilot wasn't large enough to prove anything statistically it indicates that users quickly starts trusting automated data if an initial subset of it is of high quality.

If you want to know more about the entire project that was much larger then this pilot [there is plenty for you to read](https://meta.wikimedia.org/wiki/Wikimedia_Commons_Data_Roundtripping#Links_to_key_documents).
