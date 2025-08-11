---
layout: home
title: My Blog's Homepage
---

## Hello, and welcome to my blog!

I'm glad you're here. This is my space to write about various topics.

### Latest Posts

{% for post in site.posts limit:5 %}
* [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}

<style>
.search-container {
    margin-bottom: 20px;
}
#search-input {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
}
.post-list {
    list-style: none;
    padding: 0;
}
.post-list li {
    margin-bottom: 10px;
    padding: 15px;
    border: 1px solid #eee;
    border-radius: 5px;
    background-color: #fff;
}
.post-list a {
    font-size: 20px;
    font-weight: bold;
}
</style>

<div class="search-container">
    <input type="text" id="search-input" placeholder="Search blog posts...">
</div>

<ul class="post-list" id="post-list">
  {% for post in site.posts %}
    <li data-title="{{ post.title | downcase }}" data-content="{{ post.content | strip_html | strip_newlines | downcase }}">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <small>{{ post.date | date: "%B %d, %Y" }}</small>
      <p>{{ post.excerpt | strip_html | strip_newlines | truncate: 150 }}</p>
    </li>
  {% endfor %}
</ul>

<script>
document.addEventListener('DOMContentLoaded', function() {
    const searchInput = document.getElementById('search-input');
    const postItems = document.querySelectorAll('#post-list li');

    searchInput.addEventListener('input', function(e) {
        const query = e.target.value.toLowerCase().trim();

        postItems.forEach(item => {
            const title = item.dataset.title;
            const content = item.dataset.content;

            if (title.includes(query) || content.includes(query)) {
                item.style.display = 'block';
            } else {
                item.style.display = 'none';
            }
        });
    });
});
</script>

 
