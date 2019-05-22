---
layout: page
title: 登高而招，臂非加长也，而见者远;顺风而呼，声非加疾也，而闻者彰。
description: 假舆马者，非利足也，而致千里;假舟楫者，非能水也，而绝江河。君子生(xìng)非异也，善假于物也。
keywords: 收藏
comments: true
menu: 收藏
permalink: /favorite/
---

> If I have been able to see further, it was only because I stood on the shoulders of giants. - Newton

<section class="container posts-content">
{% assign sorted_favorites = site.favorites | sort %}
{% for favor in sorted_favorites %}
<h3>{{ favor | first }}</h3>
<ol class="posts-list" id="{{ favor[0] }}">
{% for link in favor.last %}
* [{{ link.name }}]({{ link.url }})
</li>
{% endfor %}
</ol>
{% endfor %}
</section>
<!-- /section.content -->
