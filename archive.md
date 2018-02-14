---
layout: default
title: "Archive"
---

<div class="post">
<h2 class="pageTitle">Archive</h2>
{% assign postsByYearMonth = site.posts | group_by_exp:"post", "post.date | date: '%Y %b'"  %}
{% for yearMonth in postsByYearMonth %}
  <h3>{{ yearMonth.name }}</h3>
    <ul class="posts">
      {% for post in yearMonth.items %}
        <li>
          <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
          <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
      {% endfor %}
    </ul>
{% endfor %}
</div>
