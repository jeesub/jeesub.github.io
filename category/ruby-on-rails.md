---
layout: default
---

# Ruby on Rails 카테고리의 글

<ul>
  {% for post in site.categories.ruby-on-rails %}
  <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
