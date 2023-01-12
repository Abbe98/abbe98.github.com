---
layout: post
title: Writing Structured Data on Commons with Python
description: In this post, I introduce the reader to how one can write structured data to Wikimedia Commons.
image: https://byabbe.se/assets/sdc-logo.png
tags:
  - wikimedia
  - python
---
[Pywikibot does not yet have built-in support for writing Structured Data to Wikimedia Commons](https://phabricator.wikimedia.org/T223820) so to do so currently one needs to do it by posting JSON data to the Wikimedia Commons Wikibase API, this blog post will walk you through how to make the requests needed and how to structure the JSON to get it all working.

The minimal example presented here will check if the given file has a statement claiming that it depicts a hat and if not write such a statement.

First of you will need to have [Pywikibot installed and all god to go](https://www.mediawiki.org/wiki/Manual:Pywikibot/Create_your_own_script), the following imports and code should run without error.

<pre><code class="language-python">import json

import pywikibot

site = pywikibot.Site('commons', 'commons')
site.login()
site.get_tokens('csrf') # preload csrf token
</code></pre>

Next up let's turn a pagename/filename into a MID, think of a MID as Wikidata's QID but for Wikimedia Commons. The MID happens to correspond to Mediawiki's "pageid".

<pre><code class="language-python">page = pywikibot.Page(site, title='Konst och Nyhetsmagasin för medborgare af alla klasser 1818, illustration nr 44.jpg', ns=6)

media_identifier = 'M{}'.format(page.pageid)
</code></pre>

Next up, we need to fetch all existing structured data so that we can check what statements already exist. Here is the first example where we need to use Pywikibot's internal API wrapper "_simple_request" to call the Wikibase API, you could do the same with a regular HTTP library such as requests.

<pre><code class="language-python">request = site._simple_request(action='wbgetentities', ids=media_identifier)
raw = request.submit()
existing_data = None
if raw.get('entities').get(media_identifier).get('pageid'):
  existing_data = raw.get('entities').get(media_identifier)
</code></pre>

Next, let us check if depicts (P180) got a statement with the value Q80151 (hat), if so exit the program.

<pre><code class="language-python">depicts = existing_data.get('statements').get('P180')
# Q80151 (hat)
if any(statement['mainsnak']['datavalue']['value']['id'] == 'Q80151' for statement in depicts):
  print('There already exists a statement claiming that this media depicts a hat.')
  exit()
</code></pre>

Now we need to create the JSON defining such a claim, it's verbose, to say the least. You can add more claims by appending more objects to the "claims" array. To get an idea of what these JSON structures can look like you can add structured data using the Wikimedia Commons GUI and then [look at the resulting JSON by appending ".json" to the media's URI](https://commons.wikimedia.org/wiki/Special:EntityData/M39190758.json). It might be particularly interesting to try out qualifiers and references.

<pre><code class="language-python">statement_json = {'claims': [{
  'mainsnak': {
    'snaktype':'value',
    'property': 'P180',
    'datavalue': {
      'type' : 'wikibase-entityid',
      'value': {
        'numeric-id': '80151',
        'id' : 'Q80151',
      },
    },
  },
  'type': 'statement',
  'rank': 'normal',
}]}
</code></pre>

Now, all we need to do is to send this data to the Wikibase API together with some additional information such as a CSRF token the media identifier, etc.

<pre><code class="language-python">csrf_token = site.tokens['csrf']
payload = {
  'action' : 'wbeditentity',
  'format' : u'json',
  'id' : media_identifier,
  'data' : json.dumps(statement_json, separators=(',', ':')),
  'token' : csrf_token,
  'summary' : 'adding depicts statement',
  'bot' : True, # in case you're using a bot account (which you should)
}

request = site._simple_request(**payload)
try:
  request.submit()
except pywikibot.data.api.APIError as e:
  print('Got an error from the API, the following request were made:')
  print(request)
  print('Error: {}'.format(e))
</code></pre>

That should be it, you can now use this example to create your own wrapper around this functionality to make it usable in batch operations. 

In case you want to write SDC with the mwoauth/mwapi libraries instead of Pywikibot you can look at [this Flask application](https://github.com/riksantikvarieambetet/nordiska-depicts-roundtripping/blob/master/app.py#L143-L164) built for the [Roundtripping project](https://meta.wikimedia.org/wiki/Wikimedia_Commons_Data_Roundtripping) to get a hint.