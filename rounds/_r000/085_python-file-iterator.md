---
layout: post
title: Python file iterator
date: 2020-07-21 11:30:50 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example function for iterating over lines of a file
time_to_live: 1800
category: python
---



Example function for iterating over lines of a file...


```python
def iter_file(path):
  with open(path, 'r') as fd:
    for line in fd:
      yield line
```


Usage example...


```python
for line in iter_file('/tmp/test.txt'):
  print(line, end='')
```


> Note, if `print` throws a `SyntaxError: invalid syntax`, then try importing `print` from the future, or using Python version 3+, eg...


```python
from __future__ import print_function

for line in iter_file('/tmp/test.txt'):
  print(line, end='')
```
