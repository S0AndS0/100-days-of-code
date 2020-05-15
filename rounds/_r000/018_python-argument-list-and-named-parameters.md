---
layout: post
title: Python Argument List and Named Parameters
date: 2020-05-15 11:29:38 -0700
#date_updated:  # Optional and formatted like Fri May 15 11:29:38 PDT 2020 above
description: Example of accepting argument list before keyword parameters
time_to_live: 1800
---



Example of accepting argument list before keyword parameters...


```python
def fn(*args, **kwargs):
  if len(args) == 0:
    raise Exception('No args provided!')
  print("args -> {}".format(args))
  print("kwargs.get('ham') -> {}".format(kwargs.get('ham')))


fn('spam', 'flavored', ham = 'jam')
#> args -> ['spam', 'flavored']
#> kwargs.get(ham) -> jam

fn()
#> Traceback (most recent call last):
#>   File "<stdin>", line 1, in <module>
#>   File "<stdin>", line 3, in fn
#> Exception: No args provided!
```
