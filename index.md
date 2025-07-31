---
layout: page
# title: "User Manual"
---

<img src="https://avatars.githubusercontent.com/u/183564407?s=400&u=5a042a89b1f95228009942870a9e40217555c543&v=4" alt="logo" width="200" />


# User Manual

Welcome to the <a href="{{ site.baseurl }}{% post_url 2025-07-25-sonar_viz_bot_user_manual %}"> <b>user manual</b> </a> for the training project...


<div class="box-grid">
  <a class="tech-box" href="{{ site.baseurl }}{% link temp/2025-07-22-software_setup.md %}">
    <span>Software Setup</span>
  </a>
  <a class="tech-box" href="{{ site.baseurl }}{% link temp/2025-07-22-mechanical_setup.md %}">
    <span>Mechanical Setup</span>
  </a>
  <a class="tech-box" href="{{ site.baseurl }}{% link temp/2025-07-22-electrical_setup.md %}">
    <span>Electrical Setup</span>
  </a>
</div>

# Projects

See our robots


<div class="box-grid">
  <a class="tech-box" href="{{ site.baseurl }}{% post_url 2025-07-30-mobile-ros-robot %}">
    <span>Mobile ROS Robot</span>
  </a>
  <a class="tech-box" href="{{ site.baseurl }}{% post_url 2025-07-30-sonar-viz-bot %}">
    <span>Sonar Viz Bot</span>
  </a>
  <a class="tech-box" href="{{ site.baseurl }}{% post_url 2025-07-30-mars-rover %}">
    <span>Mars Rover</span>
  </a>
  <a class="tech-box" href="{{ site.baseurl }}{% post_url 2025-07-30-kiborpc %}">
    <span>KiboRPC</span>
  </a>
</div>


## Recent Posts

<ul>
  {% for post in site.posts reversed %}
    <li>
      <a href="{{site.baseurl}}{{ post.url }}">{{ post.title }}</a> – {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endfor %}
</ul>


