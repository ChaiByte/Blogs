---
layout:     page
title:      "Archives"
---

> The best way to understand a person is to listen to that person directly.

<style type="text/css">
.tags {
  overflow: hidden;
  white-space: nowrap;
}

.tag-button {
  display: inline-block;
  padding: 2px;
  margin-right: 1px;
  background-color: #ECECEC;
  font-size: 0.8em;
  border: 1px solid transparent;
  border-radius: 5px;
}
</style>

{% assign categories = site.categories | sort %}

<p>
  Jump to Category 👉
  {% for category in categories %}
    <a href="#{{ category[0] | slugify }}">[{{ category[0] | capitalize }}]</a>
  {% endfor %}
</p>

<div>
  {% for category in categories %}
    <h2>{{ category[0] | capitalize }}</h2> <!-- 这会显示分类的名称 -->
    <ul>
      {% for post in category[1] %}
        <li>
          <span class="date">{{ post.date | date: "%Y-%m-%d" }} </span>
          <span class="title"><a href="{{ post.url }}">{{ post.title }}</a></span>
          {% if post.tags.size > 0 %}
            <span class="tags">
              {% for tag in post.tags %}
                <span class="tag-button">{{ tag | downcase }}</span>
              {% endfor %}
            </span>
          {% endif %}
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>