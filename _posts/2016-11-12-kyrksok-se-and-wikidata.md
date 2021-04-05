---
layout: post
title: Kyrksok.se and Wikidata
description: Kyrksok.se links together various sources such as Wikipedia, Commons and Bebyggelseregistret and makes their content more accessible and discoverable.
image: https://byabbe.se/assets/kyrksok.png
tags:
  - wikimedia
redirect_from:
  - /blog/2016/11/12/kyrksok-se-and-wikidata
---
![The Kyrksok logo](https://byabbe.se/assets/kyrksok.png)

A few weekends ago [Jan Ainali][0], [Lars Lundqist][1], Ulrika Nilsson, David Zardini and myself attended the Hack4Heritage hackathon in Stockholm. We ended up creating the site [Kyrksok.se][2], a directory for churches in Sweden.

Kyrks&ouml;k links together various sources such as [Wikipedia][3], [Commons][4] and [Bebyggelseregistret][5] and makes their content more accessible and discoverable.

Setting up a site and display content is never that interesting or much of a challenge not even if there is content from a lot of different sources as long as there is links between them.

Guess what,

there was no such links,

Luckily Wikidata is a perfect place to link all the datasets together.

Actually most of the time spent on Kyrksok was spent on linking Bebyggelseregistret to Wikidata and on the existing data, mostly common tasks such as normalizing labels and verifying existing statements and links.

Once all the third-party URIs was in Wikidata, we could fetch a list of churches which had the required data using Wikidatas SparQL endpoint(Kyrksok query\: [visualized][7]/[source][6]).

By using Pywikibot and [KSamsok-PY][9] we could then index data from all the data sources we needed without much work. Everything was indexed to a SQLite file. That's  mainly it, we had by then a great dataset indexed form a bunch of different sources.

We then fired up a rest API(Python/Flask) for this SQLite file with both search/bounding box methods, still this API is made in less the 80 lines of code. [Just check it out][8].

The best thing about this is that this approach can be applied to any idea, the data in Wikidata is extremely diverse. Wikidata has become a incredible important source for many of the project I'm involved in including Biocaching.

Go ahead and check out all the Kyrks&ouml;k repositories over at [Github][10].

(Kyrks&ouml;k = "church search")

[0]: http://ainali.com/
[1]: https://arkland.wordpress.com/
[2]: http://kyrksok.se/

[3]: https://sv.wikipedia.org/wiki/Portal:Huvudsida
[4]: https://commons.wikimedia.org/wiki/Main_Page
[5]: http://www.bebyggelseregistret.raa.se/bbr2/sok/search.raa
[6]: https://github.com/Kyrkosok/database/blob/master/churches.rq
[7]: https://query.wikidata.org/#SELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3Flocation%20%3Farticle%20%3Fkulturarvsdata%20WHERE%20%7B%0A%20%20%23defaultView%3AMap%0A%0A%20%20%23%20get%20all%20instance%20of%20subclass%20of%20church%0A%20%20%3Fitem%20wdt%3AP31%20%3Fchurchsub%20.%0A%20%20%3Fchurchsub%20wdt%3A279%2a%20wd%3AQ16970%20.%0A%20%20%23%20with%20country%20set%20to%20Sweden%0A%20%20%3Fitem%20wdt%3AP17%20wd%3AQ34%20.%0A%20%20%23%20which%20has%20a%20kulturarvsdata%20URI%20set%0A%20%20%3Fitem%20wdt%3AP1260%20%3Fkulturarvsdata%20.%0A%20%20%23%20...a%20coordinate%20location%0A%20%20%3Fitem%20wdt%3AP625%20%3Flocation%20.%0A%0A%20%20%23%20and%20a%20sv.wikipedia%20article%0A%20%20%3Farticle%20schema%3Aabout%20%3Fitem%20.%0A%20%20%3Farticle%20schema%3AinLanguage%20%22sv%22%20.%0A%20%20%3Farticle%20schema%3AisPartOf%20%3Chttps%3A%2F%2Fsv.wikipedia.org%2F%3E%20.%0A%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP373%20%3FcommonsCategory%20.%0A%20%20%7D%0A%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP18%20%3Fimage%20.%0A%20%20%7D%0A%0A%20%20%23%20label%20it%20or%20the%20world%20turns%20into%20hell%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22sv%22%20.%20%0A%20%20%7D%0A%7D
[8]: https://github.com/Kyrkosok/api/blob/master/app.py
[9]: https://github.com/Abbe98/KSamsok-py
[10]: https://github.com/Kyrkosok