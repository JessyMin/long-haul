---
layout: default
title: "Archive"
---

<div class="post">
<h2 class="pageTitle">Archive</h2>

<ul class="posts">
{% for post in paginator.posts %}
  <li>
    <span class="date">{{ post.date | date: "%B %-d, %Y" }}</span>
    <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
  </li>
{% endfor %}
</ul>
</div>
