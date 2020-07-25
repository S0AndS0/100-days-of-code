---
layout: post
title: JavaScript `String.indexOf()` tricks
date: 2020-05-18 14:38:24 -0700
#date_updated:  # Optional and formatted like 'date' above
description: '`String.indexOf()` returns first index of target character(s) within a string'
time_to_live: 1800
category: javascript
---



In JavaScript `String.indexOf()` returns first index of target character(s) within a string...


```javascript
'555555565565'.indexOf(65);
//> 7
```


... this can be used to check `if` specific character(s) exist...


```javascript
var str = '555555565565';
var target = '65';

if (str.indexOf(target) >= 0) {
  console.log(`Found ${target} within ${str}`);
}
```


Note however, to check `if` target character(s) exist at the beginning or end of a string, the `String.endsWith()` and `String.startsWith()` methods are usually a better choice...


```javascript
var str = '123456';

if (str.startsWith(1)) {
  console.log(`${str} starts with 1 or "1"`);
}

if (str.endsWith(6)) {
  console.log(`${str} ends with 6 or "6"`);
}
```


One additional thing to remember is that for all three of these methods types are coerced.


## Attribution


- [Twitter -- @lou_alcala provided correction of `>=`](https://twitter.com/lou_alcala/status/1262537125695819782)
