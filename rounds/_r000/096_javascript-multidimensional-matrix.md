---
layout: post
title: JavaScript multidimensional matrix
date: 2020-08-01 15:39:00 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Function for generating multidimensional matrices
time_to_live: 1800
---



Function for generating multidimensional matrices...


```javascript
function makeMatrix(dimensions, size, depth) {
  depth = depth? depth: dimensions;
  return depth === 1? Array(size).fill(0).map((_, i) => i): (() => {
    const results = [];
    for (let i = 0; i < dimensions; i++) {
      results.push(makeMatrix(dimensions, size, depth - 1));
    }
    return results;
  })();
}
```


Example usage...


```javascript
const matrix = makeMatrix(4, 4)

console.log(matrix[0][1][2][3])
//> 3
```
