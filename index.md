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


### Scripting

<div class="flex-container">
    <a href="google.com">
        <div>
            test
            <span>Python</span>
        </div>
    </a>
</div>


# Changelog

_7/26/25_
- Added `main.scss` for [custom CSS](https://github.com/jekyll/minima/blob/v2.5.1/README.md#customization) overrides
- Updated [1.4 OCR Docker]({% link temp/2025-07-22-software_setup.md %}#14-ocr-docker) notes


[Software Setup]({% link temp/2025-07-22-software_setup.md %})



