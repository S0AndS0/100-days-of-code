---
layout: post
title: JavaScript `async` callback example
date: 2020-05-28 11:16:43 -0700
#date_updated:  # Optional and formatted like Thu May 28 11:16:43 PDT 2020 above
description: Both `Array.map()` and `Array.forEach()` methods are Asynchronous compatible
time_to_live: 1800
---



Both `Array.map()` and `Array.forEach()` methods are Asynchronous compatible...


```javascript
async function addLatter(number) {
  return number * 2;
}

async function listOfPromises(amount) {
  return Array(amount).fill().map(async (_, index) => {
    return addLatter(index);
  });
}


listOfPromises(3).then((result) => {
  const results = [];
  result.forEach(async (item) => {
    results.push(await item);
  });
  console.log(results);
}).catch((e) => {
  console.error(e);
});
```


... the above is shared because more than one tutorial has stated that `forEach` cannot _`await`_.
