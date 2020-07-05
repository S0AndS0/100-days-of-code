---
layout: post
title: Python exception defaulting
date: 2020-07-05 11:17:40 -0700
#date_updated:  # Optional and formatted like Sun Jul  5 11:17:40 PDT 2020 above
description: Example of handling specific exception type and defaulting
time_to_live: 1800
---



Example of handling specific exception type and defaulting...


```python
def first(arr, default = None):
  try:
    return arr[0]
  except IndexError as e:
    return default
```


Example usage...


```python
first([3, 2, 1])
#> 3

first([])
#> None

first(2)
#> TypeError: 'int' object has no attribute '__getitem__'
```


## Attribution
[heading__attribution]: #attribution


- [Python Wiki -- Handling Exceptions](https://wiki.python.org/moin/HandlingExceptions)
