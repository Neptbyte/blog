---
layout: page
title: All Posts
permalink: /allposts/
---

<style>
.post-list li {
    list-style: none;
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #eee;
    border-radius: 5px;
    background-color: #fff;
    transition: all 0.3s ease;
}
.post-list li:hover {
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}
.post-list h3 {
    margin-top: 0;
}
.filter-options {
    margin-bottom: 20px;
}
.filter-options button {
    margin: 0 5px 5px 0;
    padding: 8px 12px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    cursor: pointer;
    border-radius: 5px;
}
.filter-options button.active {
    background-color: #007bff;
    color: white;
    border-color: #007bff;
}
</style>

<div class="filter-options">
  <h3>Filter by Category:</h3>
  <button data-filter="all" class="active">All</button>
  {% assign all_categories = site.posts | map: 'categories' | join: ',' | split: ',' | uniq | sort %}
  {% for category in all_categories %}
    <button data-filter="{{ category | slugify }}">{{ category }}</button>
  {% endfor %}
</div>

<ul class="post-list" id="post-list">
  {% for post in site.posts %}
    <li data-categories="{% for category in post.categories %}{{ category | slugify }} {% endfor %}">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <small>{{ post.date | date: "%B %d, %Y" }}</small>
      <p>{{ post.excerpt | strip_html | strip_newlines | truncate: 150 }}</p>
      {% if post.categories %}
        <small><strong>Categories:</strong> 
        {% for category in post.categories %}
          <span>{{ category }}</span>{% unless forloop.last %}, {% endunless %}
        {% endfor %}
        </small>
      {% endif %}
    </li>
  {% endfor %}
</ul>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const filterButtons = document.querySelectorAll('.filter-options button');
  const postItems = document.querySelectorAll('#post-list li');

  filterButtons.forEach(button => {
    button.addEventListener('click', function() {
      // Remove 'active' class from all buttons
      filterButtons.forEach(btn => btn.classList.remove('active'));
      // Add 'active' class to the clicked button
      this.classList.add('active');

      const filter = this.dataset.filter;

      postItems.forEach(item => {
        if (filter === 'all' || item.dataset.categories.includes(filter)) {
          item.style.display = 'block';
        } else {
          item.style.display = 'none';
        }
      });
    });
  });
});
</script>
 
