---
layout: post
title: Liquid comment gotcha
date: 2020-07-08 11:05:01 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Warning `capture` blocks will interpret code within `comments`
time_to_live: 1800
---



Warning `capture` blocks will execute code within `comments`, eg...


{% raw %}
```Liquid
{% capture captured %}
{% comment %}
{% assign variable = ... %}
{% endcomment %}
{{ variable }}
{% endcapture %}
{{ captured }}
```
{% endraw %}


... the above will produce warning/error similar to...


{% raw %}
```
Liquid syntax error (line 22): [:dotdot, ".."] is not a valid expression in in "{{... }}"
```
{% endraw %}


However, code within `comment` blocks are **not** executed...


{% raw %}
```Liquid
{% capture captured %}
{% comment %}
{% assign variable = 'value' %}
{% endcomment %}
> Some {{ variable }} value
{% endcapture %}
{{ captured }}

```
{% endraw %}


... example output...


{% capture captured %}
{% comment %}
{% assign variable = 'value' %}
{% endcomment %}
> Some {{ variable }} value
{% endcapture %}
{{ captured }}
