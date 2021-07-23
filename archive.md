---
layout: page
title: Archive
permalink: /archive/
---

<section class="archive">

{% assign posts = site.posts | sort: 'date' | reverse %}
  {% for post in posts %}
  {% assign currentdate = post.date | date: "%B %Y" %}
  {% if currentdate != date %}
    {% unless forloop.first %}</ul>{% endunless %}
    <div class="month" id="y{{post.date | date: "%Y"}}">{{ currentdate }}</div>
    <ul>
    {% assign date = currentdate %}
  {% endif %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% if forloop.last %}</ul>{% endif %}
  {% endfor %}

</section>