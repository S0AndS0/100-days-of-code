---
layout: post
title: Sass array gotchas
date: 2020-07-14 11:42:55 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Array index addresses start at `1` not `0`
time_to_live: 1800
category: sass
---



Array index addresses start at `1` not `0`...


```scss
$array: (1, 2, 3);
@for $i from 1 through length($array) {
  @debug "$array[#{$i}] -> #{nth($array, $i)}";
}
```


... and `through` keyword is inclusive of the last value for a range.


___


## Attribution
[heading__attribution]: #attribution


- [Sass Language -- `@for`](https://sass-lang.com/documentation/at-rules/control/for)
