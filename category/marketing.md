---
layout: default
---

# Marketing 카테고리의 글

<ul>
  {% for post in site.categories.marketing %}
  <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
