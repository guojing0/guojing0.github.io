---
layout: for-index
title: Writings
---

{% for post in site.posts %}
  {% capture postmonth %}{{ post.date | date: "%B" }}{% endcapture %}
  {% capture postyear %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% if postmonth != month or postyear != year %}
    {% assign month = postmonth %}
    {% assign year = postyear %}
    {% if forloop.first %}
    {% else %}
    </ul>
    {% endif %}

<h2>{{ month }}{{ year}}</h2>

<ul>
  {% endif %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>&nbsp;
      <time datetime="{{post.date | date: "%Y-%m-%d"}}">
       {{ post.date | date: "%B %e, %Y" }}
     </time></li>
  {% endfor %}
</ul>