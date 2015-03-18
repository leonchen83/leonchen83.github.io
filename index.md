---
layout: page
title: SOD蜜的主页
tagline: 程序员自说自话的地方 
---
{% include JB/setup %}

## 最近的博客  

<ul class="posts">
  {% for post in site.posts limit: 15%}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
