---
layout: post
title: JavaScript objectify cookies
date: 2020-06-19 10:53:20 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Function that converts browser cookie string into JavaScript Object
time_to_live: 1800
---



Function that converts browser cookie string into JavaScript Object...


```javascript
function objectifyCookies() {
  return document.cookie.split(';').reduce((accumulator, data) => {
    const key_value = data.split('=');
    const key = key_value[0].trim();
    const value = key_value[1].trim();
    accumulator[key] = value;
    return accumulator;
  }, {});
};
```


Example usage...


```javascript
let cookies = objectifyCookies();

console.log(cookies['night_mode']);
//> "1"
```
