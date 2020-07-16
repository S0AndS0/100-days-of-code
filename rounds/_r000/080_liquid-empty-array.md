---
layout: post
title: Liquid empty array
date: 2020-07-16 11:51:26 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of how to initialize and append to an empty Liquid list
time_to_live: 1800
---



Example of how to initialize and append to an empty Liquid list...


{% raw %}
```liquid
{% assign list = '' | split: ',' %}

{% for index in (0..4) %}
  {% assign item = index | times: 2 %}
  {% assign list = list | push: item %}
{% endfor %}

<p>{{ list | join: " " }}</p>
```
{% endraw %}


Example output...


```
2 4 6 8
```
