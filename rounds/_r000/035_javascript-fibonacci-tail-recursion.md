---
layout: post
title: JavaScript Fibonacci Tail Recursion
date: 2020-06-01 10:24:12 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example calculating Fibonacci sequence using tail recursion
time_to_live: 1800
---



Example calculating Fibonacci sequence using tail recursion


```javascript
/**
 * @param {number} depth - positive number that limits recursion
 * @param {number[]} accumulator - mutable list of results
 * @param {number} value - latest value to shift from
 */
function fibonacci(depth, accumulator, value) {
  if (depth === 0) {
    return accumulator;
  }
  const last_value = accumulator.slice(-1)[0]? accumulator.slice(-1)[0]: 0;
  accumulator.push(value);
  return fibonacci(depth - 1, accumulator, last_value + value);
}
```


Example usage...


```javascript
fibonacci(10, [], 1);
//> [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

fibonacci(8, [21, 34], 55);
//> [21, 34, 55, 89, 144, 233, 377, 610, 987, 1597]
```


Tail recursion isn't always possible, but when available it should be used because tail recursion can be much more memory efficient than nested recursion.
