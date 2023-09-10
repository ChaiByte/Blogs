---
layout:     page
title:      "Archives"
---

<style type="text/css">
.tags {
  overflow: hidden;
  white-space: nowrap;
}

.tag-button {
  display: inline-block;
  padding: 0px 2px;
  margin-right: 1px;
  background-color: #ECECEC;
  font-size: 0.8em;
  border: 1px solid transparent;
  border-radius: 5px;
}
</style>

{% assign categories = site.categories | sort %}

<p>
  Filter 👉
  <a href="#" class="category-link" id="show-all">[All]</a>
  {% for category in categories %}
    <a href="#{{ category[0] | slugify }}" class="category-link">[{{ category[0] | capitalize }}]</a>
  {% endfor %}
</p>

<div>
  {% for category in categories %}
    <h2 id="{{ category[0] | slugify }}">{{ category[0] | capitalize }}</h2>
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

<script>
document.addEventListener("DOMContentLoaded", function () {
  var categoryLinks = document.querySelectorAll(".category-link");
  var categories = document.querySelectorAll("h2");

  categoryLinks.forEach(function (link) {
    link.addEventListener("click", function (event) {
      event.preventDefault();

      var targetCategory = link.getAttribute("href").substring(1);

      function showCategory(category) {
        category.style.display = "block";
        var targetList = category.nextElementSibling;
        if (targetList && targetList.tagName === "UL") {
          targetList.style.display = "block";
        }
      }

      function hideCategory(category) {
        category.style.display = "none";
        var otherList = category.nextElementSibling;
        if (otherList && otherList.tagName === "UL") {
          otherList.style.display = "none";
        }
      }

      if (targetCategory === "") { // Check if it's the "All" link
        categories.forEach(showCategory);
      } else {
        categories.forEach(function (category) {
          if (category.id === targetCategory) {
            showCategory(category);
          } else {
            hideCategory(category);
          }
        });
      }
    });
  });
});

</script>