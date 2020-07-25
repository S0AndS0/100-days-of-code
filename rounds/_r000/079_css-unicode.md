---
layout: post
title: CSS Unicode
date: 2020-07-15 10:07:42 -0700
#date_updated:  # Optional and formatted like 'date' above
description: '`::before` and `::after` pseudo elements may contain Unicode'
time_to_live: 1800
category: css
---



The `content` property for `::before` and `::after` pseudo elements may contain Unicode, eg...


```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>

    <style media="screen">
      .unicode-tester::before {
        content: '\1f43c ';
      }
    </style>
  </head>
  <body>

    <span class="unicode-tester">Panda</span>

  </body>
</html>
```


Example result...


```
🐼 Panda
```
