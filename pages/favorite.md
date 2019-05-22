---
layout: page
title: 登高而招，臂非加长也，而见者远; 顺风而呼，声非加疾也，而闻者彰。
description: 假舆马者，非利足也，而致千里;假舟楫者，非能水也，而绝江河。君子生(xìng)非异也，善假于物也。
keywords: 收藏
comments: true
menu: 收藏
permalink: /favorite/
---

> If I have been able to see further, it was only because I stood on the shoulders of giants.

<section class="container posts-content">
{% assign sorted_favo = site.favo.cat | sort %}
{% for single in sorted_favo %}

{% for link in single %}
* [{{ link.name }}]({{ link.url }})
{% endfor %}

{% endfor %}
</section>
<!-- /section.content -->
