---
layout: post
title: Extending Native Context Menus with HTML 5.1 &lt;menu&gt;
description: I recently played around with Service Workers to learn.
image: https://byabbe.se/assets/context-menu-2.png
tags:
  - web technologies
  - code
---
One thing that annoys me when using the web is when some developer decided to do `preventDefault()` on `contextmenu` to replace the native context menu with some shitty app specific one, blocking my access to thing such as spellcheck, plugins, and search. It's something I believe should be avoided whenever possible. Therefor I'm a fan of the possibility to extend the native one.

It should be noted that this is only available in Firefox for the moment.

My native context menu is full of useful features\:

![screenshot](https://byabbe.se/assets/context-menu-1.png)

I added items to the context menu to my "bookshelf" now when right clicking a book you have the options to search after the book title at Amazon or Bokus.se as well as go back to byabbe.se.

Custom parts of the native context menu is defined using the `<menu>` element(`<menu>` is standardized to define menus for buttons and toolbar too), to link a `<menu>` to its container there is an `contextmenu` attribute, I added this attribute to the element containing all books as children.

<pre><code class="language-html">&lt;menu type="context" id="book-menu">
  &lt;menuitem label="Go to byabbe.se" id="byabbe-se">&lt;/menuitem>
  &lt;menu label="Search">
    &lt;menuitem label="Bokus" id="bokus-search">&lt;/menuitem>
    &lt;menuitem label="Amazon" id="amazon-search">&lt;/menuitem>
  &lt;/menu>
&lt;/menu></code></pre>

Adding actual functionality to the items is done with the regular `click` event. But in this case the action deepened upon which element(book) that the context menu had been triggered on. This was some thing I had too keep track of by another listener.

<pre><code class="language-javascript">let currentContext = '';
document.querySelectorAll('.list')[0].addEventListener('contextmenu', e => {
  let target = e.target;
  let bookContainer;
  switch (e.target.tagName) {
    case 'SPAN':
      currentContext = target.parentElement.parentElement.children[0].innerText;
      break;
    case 'P':
      currentContext = target.parentElement.children[0].innerText;
      break;
    case 'B':
      currentContext = target.parentElement.children[0].innerText;
      break;
    case 'LI':
      currentContext = target.children[0].innerText;
      break;
    default:
      currentContext = target.innerText;
  }
});

document.querySelector('#amazon-search').addEventListener('click', e => {
  document.location = 'https://www.amazon.com/s?field-keywords=' + currentContext;
});

document.querySelector('#bokus-search').addEventListener('click', e => {
  document.location = 'http://www.bokus.com/cgi-bin/product_search.cgi?search_word=' + currentContext;
});</code></pre>

You can try it out in Firefox over at [byabbe.se/books/](https://byabbe.se/books/).

![screenshot](https://byabbe.se/assets/context-menu-2.png)

I believe there at least one major flaw with the `<menu>` element because you add items to the root of the menu, and there is no limit to the amount of items you can define. This results in tons of possible abuses such as using custom menu items to push the browser specific ones of screen(I tried, it works). It would be a lot better for the end user if all custom items would be one level below the root.
