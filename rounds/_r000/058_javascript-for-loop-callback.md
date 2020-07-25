---
layout: post
title: JavaScript `for` loop callback
date: 2020-06-24 12:35:36 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using callbacks within `for` loop iteration
time_to_live: 1800
category: javascript
---



Example of using callbacks within `for` loop iteration...


```javascript
function increment(index) {
  if (isNaN(index)) {
    index = 0;
  }
  return index + 2;
}

function compare(a, b) {
  return a < b;
}

for (let i = 0; compare(i, 10); i = increment(i)) {
  console.log(`i -> ${i}`);
}
//> i -> 0
//> i -> 2
//> i -> 4
//> i -> 4
//> i -> 8
```


... traditionally such a `for` loop would be written as...


```javascript
for (let i = 0; i < 10; i += 2) {
  console.log(`i -> ${i}`);
}
```


... however, there is nothing stopping authors from using more complex and/or expressive code within the parenthesis of a `for` loop.
