---
layout: post
title: Liquid `where` filter
date: 2020-07-25 11:38:41 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `where` Liquid filter on a collection
time_to_live: 1800
category: liquid
---



Example of using `where` Liquid filter on a collection


{% raw %}
```liquid
{% assign collection_name = 'r000' %}
{% assign language = 'liquid' %}
{% assign filtered = site[collection_name] | where: 'category', language %}


<h2>{{ language }}</h2>
<ul>
  {% for item in filtered %}
    <li>
      <h3>
        <a href="{{ item.url | relative_url }}">{{ item.title | escape }}</a>
      </h3>
      {% if item.description %}
        <blockquote>
          {{ item.description | markdownify | remove: '<p>' | remove: '</p>' }}
        </blockquote>
      {% elsif site.show_excerpts and item.excerpt %}
        <blockquote>
          {{ item.excerpt | markdownify | remove: '<p>' | remove: '</p>' }}
        </blockquote>
      {% endif %}
    </li>    
  {% endfor %}
</ul>
```
{% endraw %}


Example HTML results...


{% assign collection_name = 'r000' %}
{% assign language = 'liquid' %}
{% assign filtered = site[collection_name] | where: 'category', language %}
```html
<h2>{{ language }}</h2>
<ul>
  {% for item in filtered %}
    <li>
      <h3>
        <a href="{{ item.url | relative_url }}">{{ item.title | escape }}</a>
      </h3>
      {% if item.description %}
        <blockquote>
          {{ item.description | markdownify | remove: '<p>' | remove: '</p>' }}
        </blockquote>
      {% elsif site.show_excerpts and item.excerpt %}
        <blockquote>
          {{ item.excerpt | markdownify | remove: '<p>' | remove: '</p>' }}
        </blockquote>
      {% endif %}
    </li>    
  {% endfor %}
</ul>
```


Example output


{% assign collection_name = 'r000' %}
{% assign language = 'liquid' %}
{% assign filtered = site[collection_name] | where: 'category', language %}
<h2>{{ language }}</h2>
<ul>
  {% for item in filtered %}
    <li>
      <h3>
        <a href="{{ item.url | relative_url }}">{{ item.title | escape }}</a>
      </h3>
      {% if item.description %}
        <blockquote>
          {{ item.description | markdownify | remove: '<p>' | remove: '</p>' }}
        </blockquote>
      {% elsif site.show_excerpts and item.excerpt %}
        <blockquote>
          {{ item.excerpt | markdownify | remove: '<p>' | remove: '</p>' }}
        </blockquote>
      {% endif %}
    </li>    
  {% endfor %}
</ul>


{% comment %}

{% endcomment %}
