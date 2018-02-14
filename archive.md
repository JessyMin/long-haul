---
layout: default
title: "Archive"
---

<div class="post">
<h2 class="pageTitle">Archive</h2>
<h3>{{ page.date | date: "%Y" }}</h3>  

<ul class="posts noLists">
  {% for post in page.posts %}
    <li>
      <span class="date">{{ post.date | date: "%B %-d, %Y" }}</span>
      <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
</div>
