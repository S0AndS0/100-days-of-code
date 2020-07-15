---
layout: post
title: Bash Parameter Transformation
date: 2020-06-14 11:04:20 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using Bash Parameter Transformation options to prevent expansion
time_to_live: 1800
---



Example of using Bash Parameter Transformation options to prevent expansion...


```bash
_variable="thing$ remain quoted"
echo "${_variable@Q}"
#> 'thing$ remain quoted'
```

... the _`@Q`_ bits are the _magic sauce_ which let the shell know that the string should **not** be expanded, ie. sub-shells and/or variables are **not** interpreted, find more via...


```bash
man -P 'less -p "^ +Parameter +transformation"' bash
```
