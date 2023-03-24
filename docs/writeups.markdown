---
layout: page
title: Write-up
---
<link rel="stylesheet" type="text/css" href="src/css/style.css">
<span>testooo</span>
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}" class="a">{{ post.title }}</a>
      <span>{{post.date | date_to_string}}</span>
      <span>{{post.categories}}</span>
    </li>
  {% endfor %}
</ul>