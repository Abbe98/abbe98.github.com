---
layout: post
title: Platsr API Sandbox
description: I made an API Sandbox for Platsr.se and introduces basic API accessibility.
image: https://byabbe.se/assets/p-sandbox1.png
tags:
  - code
---
**Update** Platsr.se does no longer exists.

[Platsr.se][0] if you aren't familiar is a web community for gathering local stories and media around different locations. As a result it got some pretty incredible data, which users have put a lot of thought into, all available under open licenses.

Platsr also got a API and have been having one for ages, but almost no one has created upon it. If you [take a look at the official documentation][1] you won't find that fact weird(even if you do read Swedish).

Only because you provide an open API you do not make it accessible. Actually, you can throw huge piles of money into developing an amazing API and developers will never end up using it anyway.

### Creating Something Useful

I decided to rewrite the Platsr API documentation and create an API Sandbox for it.

When I set off to build the sandbox my feature specification was as basic as the following\:

 - Visual interface for geographic queries, bounding boxes, etc.
 - Tied closely with the documentation for usability.
 - Only relevant parameter fields for your specific query should be displayed.
 - Users should be able to share queries with direct links.
 - Resources within the response body should link to its sandbox query.

Rewriting all the documentation from scratch took a train trip between Oslo and Katrineholm(roughly five hours). Nothing the original developers could not have invested in from the beginning.

Building the sandbox on the other hand took a lot more time than it would have taken me to write the actual API.

It required a proxy server to avoid CORS and Mixed Content issues, because who uses your API clientside and prefers HTTPS? ;-)

In the end I ended up being relay happy about the end result, you can [try the sandbox out and access the documentation right now][2]. Please let me know what you think so I can make even better sandboxes and documentation next time! 

Tip: When developing APIs write the documentation first then use it as a blueprint for the actual development.

**Want to chat?**

Would you like to talk to me about open data/data accessibility, hacks/projects, or anything else?

I will be attending both [Hack4Heritage][3] in Stockholm and [Hack4NO][4] in H&oslash;nefoss, make sure to catch me there!

![Screenshot](https://byabbe.se/assets/p-sandbox1.png)
![Screenshot](https://byabbe.se/assets/p-sandbox2.png)

**Some previous  posts that might interest you\:**

 - [Digging Deeper with Heritage Data and a Geocoder][5]
 - [K-Sams&ouml;k-PHP the Basics][6]
 - [K-Sams&ouml;k-PHP Advanced Usage][7]

[0]: http://www.platsr.se/platsr/
[1]:  http://www.platsr.nu/platsrs-api/
[2]: https://byabbe.se/platsr-api-sandbox/index.html
[3]: https://www.raa.se/hack-for-heritage/
[4]: https://web.archive.org/web/20200224051738/http://www.hack4.no/
[5]: https://byabbe.se/2016/02/04/digging-deeper-with-heritage-data-and-a-geocoder
[6]: https://byabbe.se/2016/01/25/ksamsok-the-basics
[7]: https://byabbe.se/2016/01/26/ksamsok-php-advanced-usage
