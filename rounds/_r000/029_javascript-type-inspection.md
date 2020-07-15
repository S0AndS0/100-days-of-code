---
layout: post
title: JavaScript Type Inspection
date: 2020-05-26 10:35:24 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Function that demonstrates some messy bits of JavaScript types
time_to_live: 1800
---



Function that demonstrates some messy bits of JavaScript types...


```javascript
const whatIs = (value) => {
  if (Array.isArray(value)) {
    return 'array';
  } else if (value instanceof Object) {
    return 'object';
  } else if (typeof value === 'string') {
    return 'string';
  } else if (!isNaN(value)) {
    return 'number';
  }

  console.warn('Ambiguous type for ->', value)
  return typeof value;
};
```


**Notice**, detecting an Array before an Object, and detection of String before Number is important! Because Arrays are also Objects and number like strings are coerced to numbers by most operations.


Example usage...


```javascript
whatIs("1");
//> 'string'
whatIs(1);
//> 'number'
whatIs([]);
//> 'array'
whatIs({});
//> 'object'

whatIs(NaN);
//> ⚠️ Ambiguous type for -> NaN
//> 'number'
```
