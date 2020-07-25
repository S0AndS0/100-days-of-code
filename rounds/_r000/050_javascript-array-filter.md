---
layout: post
title: JavaScript Array Filter
date: 2020-06-16 11:02:06 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of filtering an Array for odd or even numbers
time_to_live: 1800
category: javascript
---



Example of filtering an Array for odd or even numbers...


```javascript
let array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

let evens = array.filter((i) => { return i % 2 === 0; });

let odds = array.filter((i) => { return i % 2 !== 0; });

console.log(evens);
//> [0, 2, 4, 6, 8]

console.log(odds);
//> [1, 3, 5, 7, 9]
```



## Attribution
[heading__attribution]: #attribution "Resources that where helpful in writing this post"


- [Mozilla Developer -- `Array.prototype.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
