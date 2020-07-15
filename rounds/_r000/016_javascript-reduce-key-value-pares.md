---
layout: post
title: JavaScript Reduce Key Value Pares
date: 2020-05-13 14:39:52 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of `reduce` on object `entries` for uniq key value pares
time_to_live: 1800
---



Example of `reduce` on object `entries` for uniq key value pares...


```javascript
const a = {first: 'lamb', second: 'ham', third: 'spam'};
const b = {first: 'ham', second: 'flavored'};


const uniq = Object.entries(a).reduce((acc, [k, v]) => {
  if (!Object.keys(b).includes(k)) {
    acc[k] = v;
  }
  return acc;
}, {});


console.log(uniq);
//> {third: 'spam'}
```
