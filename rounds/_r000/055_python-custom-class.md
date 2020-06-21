---
layout: post
title: Python custom class
date: 2020-06-21 10:13:51 -0700
#date_updated:  # Optional and formatted like Sun Jun 21 10:13:51 PDT 2020 above
description: Example of a custom Python class with inheritance
time_to_live: 1800
---



Example of a custom Python class with inheritance...


```python
class Custom(dict):
    def __init__(self, *args, **kwargs):
        super(Custom, self).__init__(**kwargs)
        self.update(args = args)
```


Example usage...


```python
cust = Custom('ham', 'flavored', spam = 'spicy')

print(cust)
#> {'args': ('ham', 'flavored'), 'spam': 'spicy'}
```


- `*args`, with a single asterisk, accepts list of unnamed arguments

- `**kwargs`, with a two asterisks, accepts arbitrary amount of named parameters
