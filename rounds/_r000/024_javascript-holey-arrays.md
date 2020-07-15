---
layout: post
title: JavaScript Holey Arrays
date: 2020-05-21 14:02:31 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of sanitizing empty slots
time_to_live: 1800
---



Example of sanitizing empty slots from Holey Arrays...


```javascript
const list = [];

list[0] = 1;
list[3] = 4;

console.log(list);
//> [1, <2 empty slot>, 4]


const sanitized = list.reduce((accumulator, item) => {
  accumulator.push(item);
  return accumulator;
}, []);

console.log(sanitized);
//> [1, 4]
```


## Attribution


- [v8.dev -- `PACKED` vs. `HOLEY` kinds](https://v8.dev/blog/elements-kinds#packed-vs.-holey-kinds)
