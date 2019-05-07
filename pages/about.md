---
layout: page
title: 亦余心之所善兮，虽九死其犹未悔
description: I am my own God~!
keywords: Michael Zhou
comments: true
menu: 关于
permalink: /about/
---

我是Michael Zhou, 一个测试行业的从业人员。

仰慕「优雅编码的艺术」。

坚信熟能生巧，努力改变人生。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
