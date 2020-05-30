---
layout: post
title: Python publishing `entry_points` gotcha
date: 2020-05-30 10:02:41 -0700
#date_updated:  # Optional and formatted like Sat May 30 10:02:41 PDT 2020 above
description: '`entry_points["console_scripts"]` are imported by installed scripts'
time_to_live: 1800
---



The following will always raise an Exception if configured within `entry_points["console_scripts"]` of a package `setup.py` script...


```python
if __name__ != '__main__':
    raise NotImplementedError('Try running this file as a script instead.')
```


... because scripts listed by `entry_points["console_scripts"]` are imported by installed scripts.
