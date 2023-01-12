---
layout: post
title: Rounding Colors with Colorsnap
description: Colorsnap is a Python package for snapping/rounding colors to other colors/palettes.
image: https://byabbe.se/assets/screenshot-gi-raa-color-filter.png
tags:
  - python
  - code
---

While working on an evaluation of Generous Interfaces in the GLAM sector at the Swedish National Heritage Board we extracted colors in images to make them searchable by their palettes. For usability reasons we wanted to limit the extracted colors to a comprehensible palette.

![Screenshot of our generous interface.][0]

Colorsnap is a Python package for snapping/rounding colors to other colors/palettes. Although I could find plenty of resources and examples on how to do this, I could not find a accessible package.

So now you can do\:

`pip install colorsnap`

Let's take the hex color `#0000ba` and round it to its nearest color available as a named color in the CSS 3 specification.

<pre><code class="language-python">from colorsnap.palettes import CSS_3
from colorsnap import snap_color

snap_color(CSS_3, '#0000ba')
# returns the following tuple ('#0000ba', 'mediumblue')
</code></pre>

visualized (input to the left)\:

![Colors compared.][1]

Colorsnap comes with palettes for CSS 2, 2.1, 3, and 4 but you can also use your own\:

<pre><code class="language-python">from colorsnap import snap_color

palette = {
    'black': '#000000',
    'gray': '#808080',
    'white': '#ffffff',
}

snap_color(palette, '#0000ba')
</code></pre>

In addition to using named colors you can also round colors to basic hex values\:

<pre><code class="language-python">from colorsnap import snap_color

palette = ['#4286f4', '#414449']

snap_color(palette, '#0000ba')
</code></pre>

It's available over at [PyPI][2] and [Github][3].

[0]: https://byabbe.se/assets/screenshot-gi-raa-color-filter.png
[1]: https://byabbe.se/assets/colorsnap-example.png
[2]: https://pypi.org/project/colorsnap/
[3]: https://github.com/riksantikvarieambetet/colorsnap
