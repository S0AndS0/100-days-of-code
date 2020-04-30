---
layout: post
title: JavaScript Padding Strings
date: 2020-04-29 09:41:02 -0700
#date_updated:  # Optional and formatted like Wed Apr 29 09:41:02 PDT 2020 above
description: Zero padding values with JavaScript
time_to_live: 1800
---



Zero padding values with JavaScript...


```javascript
const pad = (value, padding, amount) => {
  return (padding.toString().repeat(amount) + value).slice(-amount);
};


pad(12, 0, 3);
//> "012"


pad("spam", "🥫", 8);
//> "🥫spam"
```


Some (if not most) emoji count as two characters which is why the second example required an `amount` of `6` to retain the four characters of `"spam"`, and one `🥫` (Canned Food) emoji. Furthermore non-Roman based alphabets may also have individual characters with lengths greater than one, so the above `pad` function is likely best used with _number-like_ `value` and `padding` parameters.
