---
layout: post
title: HTML `oninput` Event
date: 2020-06-23 15:39:57 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example HTML and JavaScript for `oninput` event
time_to_live: 1800
---



Example HTML and JavaScript for `oninput` event...


```html
<input type="text" oninput="document.getElementById('oninput-output').value = event.target.value.toUpperCase();">

<br>

<input type="text" id="oninput-output" readonly>
```


Live demo...



<input type="text" oninput="document.getElementById('oninput-output').value = event.target.value.toUpperCase();">

<br>

<input type="text" id="oninput-output" readonly>
