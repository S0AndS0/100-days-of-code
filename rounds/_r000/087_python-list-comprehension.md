---
layout: post
title: Python list comprehension
date: 2020-07-23 13:01:52 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using Python list comprehension to calculate factors of integer
time_to_live: 1800
category: python
---



Example of using Python list comprehension to calculate factors of integer...


```python
from math import (sqrt, floor)

def factors(number):
  end = floor(sqrt(number)) + 1
  array = [i for i in range(1, end) if number % i == 0]
  array = array + [number // i for i in array]
  return sorted(array)
```


Example usage...


```python
factors(9)
#> [1, 3, 9]

factors(29)
#> [1, 29]
```
