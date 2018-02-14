---
layout: default
title: "Archive"
---

<div class="post">
<h2 class="pageTitle">Archive</h2>
<h3>{{ post.date | date: "%Y" }}</h3>  

<ul class="posts">
  {% for post in site.posts %}
    <li>
      <span class="date">{{ post.date | date: "%B %-d, %Y" }}</span>
      <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
</div>
