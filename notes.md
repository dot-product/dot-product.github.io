---
layout : default
title : Notes
---

{% include home_index.html%}
<ul>
  {% for page in site.My_Notes %}
    <li>
      <h2><a href="{{ page.url }}">{{ page.title }}</a></h2>
    </li>
  {% endfor %}
</ul>
