---
layout: post
title: Python from Math summation
date: 2020-06-05 13:59:07 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of translating Math summation to Python syntax
time_to_live: 1800
mathjax: true
---



Example of translating Math summation to Python syntax...


$$
\sum\limits_{n=1}^{10}2_{n}
$$


```python
n = 1
total = 0
while n <= 10:
  total += 2 * n
  n += 1

print(total)
```


... this is but one way to translate ∑ (summation) into Python code.
