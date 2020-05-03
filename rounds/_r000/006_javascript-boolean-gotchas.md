---
layout: post
title: JavaScript Boolean Gotchas
date: 2020-05-03 11:39:59 -0700
#date_updated:  # Optional and formatted like Sun May  3 11:39:59 PDT 2020 above
description: '`true` is coerced to a number but `"true"` is not'
time_to_live: 1800
---



JavaScript gotcha, `true` is coerced to a number but `"true"` is not...


```javascript
isNaN(true);
//> false
isNaN('true');
//> true
```


... but `JSON.parse()` coerces either...


```javascript
isNaN(JSON.parse('true'));
//> false
isNaN(JSON.parse(true));
//> false
```


... and the same is also _true_ for `false` and `"false"`
