---
layout: post
title: JavaScript character array
date: 2020-07-02 10:44:06 -0700
#date_updated:  # Optional and formatted like Thu Jul  2 10:44:06 PDT 2020 above
description: Example of using Spread Syntax in JavaScript to build character arrays
time_to_live: 1800
---



Example of using Spread Syntax in JavaScript to build character arrays...


```javascript
const food_items = [...'🍅🥓🍞'];
console.log(food_items);
//> ["🍅", "🥓", "🍞"]

const char_list = [...'a1b2'];
console.log(char_list);
//> ["a", "1", "b", "2"]
```


... the _magic sauce_ of _`[...'string']`_ splits Unicode strings at each symbol, where as _`'string'.split('')`_ will split Unicode characters into their components, eg...


```javascript
'🍅🥓🍞'.split('');
//> ["\ud83c", "\udf45", "\ud83e", "\udd53", "\ud83c", "\udf5e"]
```
