---
layout: post
title: HTML Text Direction
date: 2020-05-07 09:40:12 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Individual HTML elements can define text direction
time_to_live: 1800
---



Individual HTML elements can define text direction...



```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Text Direction Examples</title>
  </head>
  <body>
    <p dir="rtl">מימין לשמאל</p><!-- From right to left -->
    <p dir="ltr">Left to Right</p>
    <p dir="auto">Defined by browser</p>
  </body>
</html>
```


**Example results**


------


<p dir="rtl">מימין לשמאל</p>
<p dir="ltr">Left to Right</p>
<p dir="auto">Defined by browser</p>


------


... and JavaScript can assign or modify text direction via `.dir` property on HTML elements...


```javascript
{
  const p = document.createElement('p');
  p.dir = 'ltr';
  p.innerText = 'Left to Right';
  document.body.appendChild(p);
}


{
  const p = document.createElement('p');
  p.dir = 'rtl';
  p.innerText = 'מימין לשמאל';
  document.body.appendChild(p);
}
```



## Attribution


- [w3schools -- HTML dir Attribute](https://www.w3schools.com/tags/att_global_dir.asp)
