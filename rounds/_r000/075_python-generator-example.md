---
layout: post
title: Python generator example
date: 2020-07-11 11:36:16 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `yield` within a function
time_to_live: 1800
category: python
---



Example of using `yield` within a function...


```python
def counter(i, step):
  while 1:
    i += step
    yield i
```


Example usage...


```python
evens = counter(0, 2)
evens.next()
#> 2

evens.next()
#> 4


for c in counter(1, 2):
  print(c)
  if c > 7:
    break

#> 3
#> 5
#> 7
#> 9
```
