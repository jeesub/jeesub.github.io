---
layout: default
---

# etc. 카테고리의 글

<ul>
  {% for post in site.categories.etc %}
  <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
