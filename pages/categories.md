---
layout: categories
title: 物以类聚，人以群分
description: 哈哈，你找到了我的文章基因库
keywords: 分类
comments: false
menu: 分类
permalink: /categories/
---

> Birds of a feather flock together.

{% for link in site.data.links %}
* [{{ link.name }}]({{ link.url }})
{% endfor %}