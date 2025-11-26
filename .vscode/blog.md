---
layout: default
title: Blog
permalink: /blog/
---

<h1>Blog</h1>

<ul class="post-list">
  {% for post in site.posts %}
    <li class="post-card">
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
      <p>{{ post.excerpt | strip_html | truncate: 200 }}</p>
      <a class="post-link" href="{{ post.url | relative_url }}">Read more →</a>
    </li>
  {% endfor %}
  {% if site.posts.size == 0 %}
    <li>No posts yet. Once you add some, they’ll show up here.</li>
  {% endif %}
</ul>
