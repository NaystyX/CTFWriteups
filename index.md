---
layout: default
title: THM Writeups
---

{% assign pages = site.pages | where_exp: "p", "p.path contains 'writeups/'" %}
<ul>
  {% for page in pages %}
    <li><a href="{{ page.url }}">{{ page.title | default: page.name }}</a></li>
  {% endfor %}
</ul>
