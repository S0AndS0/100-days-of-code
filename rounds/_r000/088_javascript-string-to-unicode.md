---
layout: post
title: JavaScript string to Unicode
date: 2020-07-24 12:49:14 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using spread syntax and `Array().map()` for string conversion
time_to_live: 1800
category: javascript
---



Example of using spread syntax and `Array().map()` for string conversion


```javascript
function toUnicodeList(string) {
  return [...string].map((character => {
    return character.codePointAt().toString(16);
  }));
}
```


Example usage...


```javascript
toUnicodeList('🎉');
//> ["1f389"]
```
