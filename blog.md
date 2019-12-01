---
layout : default
<!-- title : dot -->
---
{% include home_index.html%}
<ul>
  <!-- {% for page in site.Python_Pages %}
    <li>
      <h2><a href="{{ page.url }}">{{ page.title }}</a></h2>
    </li>
  {% endfor %}
  {% for page in site.Algorithms %}
    <li>
      <h2><a href="{{ page.url }}">{{ page.title }}</a></h2>
    </li>
  {% endfor %}
  {% for page in site.Hadoop %}
    <li>
      <h2><a href="{{ page.url }}">{{ page.title }}</a></h2>
    </li>
  {% endfor %} -->
  {% for page in site.Linux %}
    <li>
      <h2><a href="{{ page.url }}">{{ page.title }}</a></h2>
      <!-- <p>{{ page.excerpt }}</p> -->
    </li>
  {% endfor %}

</ul>
