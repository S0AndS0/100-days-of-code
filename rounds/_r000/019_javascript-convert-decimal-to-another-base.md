---
layout: post
title: JavaScript Convert Decimal to Another Base
date: 2020-05-16 14:39:50 -0700
#date_updated:  # Optional and formatted like Sat May 16 14:39:50 PDT 2020 above
description: Using `toString()` and Bitwise operators to convert numbers
time_to_live: 1800
---



Using `toString()` and Bitwise operators to convert numbers...


```javascript
const changeBase = (decimal, radix) => {
  return (decimal >>> 0).toString(radix);
};


changeBase("3735928559", 16);
//> "deadbeef"

changeBase(123, 16);
//> "1111011"
```


Prepending number literal base that JavaScript supports...


```javascript
const convertDecimal = (decimal, radix) => {
  const result = (decimal >>> 0).toString(radix);
  if (radix == 2) {
    return `0b${result}`;
  } else if (radix == 8) {
    return `0o${result}`;
  } else if (radix == 16) {
    return `0x${result}`;
  }
  return result;
};


convertDecimal(42, 8);
//> "0o52"

convertDecimal('2e6', 6);
//> "110511132"
```



## Attribution


- [Teocci of StackOverflow -- `parseInt()` not converting decimal to binary?](https://stackoverflow.com/a/53956870)
