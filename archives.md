---
layout:     page
title:      "Archives"
---

> The best way to understand a person is to listen to that person directly.

<ul>
  {% for post in site.posts %}
    <li>
       {{ post.date | date: "%Y-%m-%d" }} <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>