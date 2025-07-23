---
layout: page
# title: "User Manual"
---

<img src="https://avatars.githubusercontent.com/u/183564407?s=400&u=5a042a89b1f95228009942870a9e40217555c543&v=4" alt="logo" width="200" />

# User Manual

Welcome to the user manual for this project...

## Recent Posts

<ul>
  {% for post in site.posts reversed %}
    <li>
      <a href="{{site.baseurl}}{{ post.url }}">{{ post.title }}</a> – {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endfor %}
</ul>
