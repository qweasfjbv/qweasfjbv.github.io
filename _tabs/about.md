---
title: About
icon: fas fa-info
order: 4

# The About page
# v2.0
# https://github.com/cotes2020/jekyll-theme-chirpy
# © 2017-2019 Cotes Chung
# MIT License
---

{{ site.categories.Algorithm | size }}

{{ site.posts | size }}

{{ site.categories.Blogging | size }}

{{ site.categories.ProblemSolving | size }}

{% for category in site.categories %}
  <h3>{{ category[0] }}</h3>
  <ul>
    {% for post in category[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}