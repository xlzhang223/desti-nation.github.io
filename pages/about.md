---
layout: page
title: About
description: Hello World
keywords: Pt
comments: true
menu: 关于
permalink: /about/
---

Pt，非典型计算机科学与技术学生，不会修电脑

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
