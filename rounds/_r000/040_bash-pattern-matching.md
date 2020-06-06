---
layout: post
title: Bash Pattern Matching
date: 2020-06-06 15:45:23 -0700
#date_updated:  # Optional and formatted like Sat Jun  6 15:45:23 PDT 2020 above
description: Example of replacing characters that are not of numeric or alphabet class
time_to_live: 1800
---



Example of replacing characters that are not of numeric or alphabet class with dashes (`-`)...


```bash
_variable='$uspicious Str!ng'

printf '%s\n' "${_variable//[^[:alnum:]]/-}"
#> -uspicious-Str-ng
```


... Check the manual pages of Bash for more Pattern Matching short-cuts that can be used in-place or addition to RegExp...


```bash
man -P 'less -p "^[[:space:]]*Pattern Matching"' bash
```
