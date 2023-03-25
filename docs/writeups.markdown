---
layout: page
title: Writeups
---
<link rel="stylesheet" href="{{ "/src/css/style.css" | relative_url }}">

<ul>
  {% for post in site.posts %}
    <li>
      <div class="article-blog">
        <a href="{{ post.url }}" class="a">{{ post.title }}</a>
        <span>{{post.date | date_to_string}}</span>
        <span class="cat-web">{{post.categories}}</span>
        <span class="easy">{{post.difficulty}}</span>
      </div>
    </li>
  {% endfor %}
</ul>