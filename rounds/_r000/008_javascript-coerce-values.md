---
layout: post
title: JavaScript Coerce Values
date: 2020-05-05 10:00:32 -0700
#date_updated:  # Optional and formatted like Tue May  5 10:00:32 PDT 2020 above
description: Convert strings to JavaScript Object types where available
time_to_live: 1800
---



JavaScript function for coercing strings to JavaScript Object types where available...


```javascript
const coerce = (value) => {
  try {
    return JSON.parse(value);
  } catch (e) {
    if (!(e instanceof SyntaxError)) {
      throw e;
    }

    if (['undefined', undefined].includes(value)) {
      return undefined;
    } else {
      return value;
    }
  }
};
```


... Simple usage examples...


```javascript
coerce('1');
//> 1

coerce('false');
//> false

coerce('undefined');
//> undefined
```


... Slightly more complex usage example...


```javascript
var coercedValue = coerce('{ "canned": {"spam": true} }');

typeof coercedValue;
//> "object"

typeof coercedValue['canned']
//> "object"

typeof coercedValue['canned']['spam']
//> "boolean"
```


... Where it currently fails to coerce values...


```javascript
var coercedValue = coerce('{ "canned": {"spam": "true"} }');

typeof coercedValue['canned']['spam']
//> "string"
```
