---
layout: page
title: 学然后知不足，教然后知困
description: 人越学越觉得自己无知
keywords: 维基, Wiki
comments: false
menu: 维基
permalink: /wiki/
---

> Chaos is a ladder.

<ul class="listing">
{% for wiki in site.wiki %}
{% if wiki.title != "Wiki Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ wiki.url }}">{{ wiki.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
