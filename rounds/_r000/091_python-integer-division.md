---
layout: post
title: Python integer division
date: 2020-07-27 10:48:15 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `//` operator instead of `math.floor()` method
time_to_live: 1800
---



Example of using `//` operator instead of `math.floor()` method...


```python
9 / 2
#> 4.5

9 // 2
#> 4
```


... if for some reason a float is needed as a result, then convert the results with the builtin `float()` function...


```python
float(7 // 2)
#> 3.0
```
