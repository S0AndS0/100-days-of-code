---
layout: post
title: Python doc-strings
date: 2020-07-30 15:20:32 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Examples of defining and accessing Python documentation
time_to_live: 1800
---



Examples of defining Python documentation string...


```python
def fn():
  """
  Documentation for this function
  """
  pass
```


Documentation for classes, methods, and functions may be accessed via `print` or `help`, eg...


```python
print(fn.__doc__)
help(fn)
```
