---
layout: for-index
title: Writings
---

<ul>
  {% for post in site.posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>&nbsp;
      <time datetime="{{post.date | date: "%Y-%m-%d"}}">
       {{ post.date | date: "%B %e, %Y" }}
     </time></li>
  {% endfor %}
</ul>