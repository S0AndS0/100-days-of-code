---
layout: post
title: Python Modulo Example
date: 2020-06-12 09:39:35 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to check if integer is even
time_to_live: 1800
---



Example function to check if integer is even...


```python
def isEven(value):
  if type(value) == int:
    return value % 2 == 0
  raise TypeError('value is not an integer')
```


Example usage...


```python
isEven(6)
#> True
isEven(7)
#> False
isEven('spam')
#> TypeError
```
