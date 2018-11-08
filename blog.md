---
layout : default
title : Python for Data Science
---

<ul>
  {% for page in site.Python_Pages %}
    <li>
      <h2><a href="{{ page.url }}">{{ page.title }}</a></h2>
    </li>
  {% endfor %}
</ul>
