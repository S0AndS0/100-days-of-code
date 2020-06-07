---
layout: post
title: JavaScript Ternary Operator
date: 2020-06-07 10:49:48 -0700
#date_updated:  # Optional and formatted like Sun Jun  7 10:49:48 PDT 2020 above
description: Example of conditional (ternary) operator within template literal
time_to_live: 1800
---



Example of conditional (ternary) operator within template literal


```javascript
for (let i = 0; i < 3; i++) {
  console.log(`${i} apple${i !== 1? 's': ''}`);
}
//> 0 apples
//> 1 apple
//> 2 apples
```


## Attribution


- [@Okegbero_Maro of Twitter -- Python format strings example](https://twitter.com/Okegbero_Maro/status/1268817975756324864)

- [Mozilla Developer -- Conditional (ternary) operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
