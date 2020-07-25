---
layout: post
title: JavaScript Fibonacci Generator
date: 2020-06-09 10:30:05 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `yield` within a function to generate Fibonacci sequence
time_to_live: 1800
category: javascript
---



Example of using `yield` within a function to generate Fibonacci sequence...


```javascript
function* fib(a, b) {
  while (1) {
    const v = a + b;
    a = b;
    b = v;
    yield v;
  }
}
```


Example usage...


```javascript
let i = 0;
for (let value of fib(0, 1)) {
  console.log(i, value);
  if (i > 9) { break; }
  i++;
}
//> 0 1
//> 1 2
//> 2 3
//> 3 5
//> 4 8
//> 5 13
//> 6 21
//> 7 34
//> 8 55
//> 9 89
//> 10 144
```
