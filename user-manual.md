---
layout: page
title: "User Manual"
permalink: /user-manual/
---

# User Manual

Welcome to the user manual for this project...

## Recent Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> – {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endfor %}
</ul>
