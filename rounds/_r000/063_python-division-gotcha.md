---
layout: post
title: Python division gotcha
date: 2020-06-29 12:21:05 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Examples of float vs integer division
time_to_live: 1800
category: python
---



Examples of float vs integer division...


```python
1 / 2
#> 0

1 / 2.0
#> 0.5

1.0 / 2
#> 0.5
```


... the `__div__` method for `float`  and `int` are different. So for functions that do Math it is a good idea to convert explicitly...


```python
def f_div(n, d):
    return float(n) / d


f_div(1, 2)
#> 0.5
```
