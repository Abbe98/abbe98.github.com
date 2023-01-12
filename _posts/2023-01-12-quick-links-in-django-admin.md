---
layout: post
title: Quick Links in Django Admin
description: By enabeling the startpage in Django Admin's startpage we can get space for various type of shortcuts and links useful to admins that fits right into Django's structure and style.
tags:
  - python
  - django
---
Whenever you are viewing a model-page in Django's admin-interface there is a sidebar to the left giving you quick access to other models:

![Screenshot of the default sidebar on a model page.](/assets/django-admin-model-sidebar.png)

This sidebar, however, isn't utilized on the start/index page. By enabeling the sidebar we can get space for various types of shortcuts and links that can be useful to admins. The sidebar will also fit right into Django's structure and style.

![Screenshot of a sidebar with quick links on Django's admin index.](/assets/django-admin-index-sidebar.png)

By creating `templates/admin/index.html` in our ocal project we can override the default admin index from Django an replace it with our own. Because the default page contains the template block hosting the navbar, even through it's unused we can extend the existing Django's template and reuse the pattern/semantics used by the sidebar eslewhere.

Here is an example creating two sidebar sections with two links each:

<pre><code class="language-html">&#123;% extends "admin/index.html" %}

&#123;% block nav-sidebar %}
&#123;% load i18n %}
&lt;button class="sticky toggle-nav-sidebar" id="toggle-nav-sidebar" aria-label="&#123;% translate 'Toggle navigation' %}"></button>
&lt;nav class="sticky" id="nav-sidebar">
    &lt;input type="search" id="nav-filter"
         placeholder="&#123;% translate 'Start typing to filter…' %}"
         aria-label="&#123;% translate 'Filter navigation items' %}">
    &lt;div class="module">
        &lt;table>
          &lt;caption>Support</caption>
            &lt;tr>
                &lt;th scope="row">&lt;a href="#">Email</a></th>
            &lt;/tr>
            &lt;tr>
                &lt;th scope="row">&lt;a href="#">Report Bug</a></th>
            </tr>
        </table>
    </div>
    &lt;div class="module">
        &lt;table>
          &lt;caption>Development</caption>
            &lt;tr>
                &lt;th scope="row">&lt;a href="#">Repository</a></th>
            </tr>
            &lt;tr>
                &lt;th scope="row">&lt;a href="#">Backlog</a></th>
            </tr>
        </table>
    </div>
</nav>
&#123;% endblock %}</code></pre>
