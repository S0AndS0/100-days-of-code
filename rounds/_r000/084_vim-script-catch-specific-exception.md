---
layout: post
title: Vim script catch specific exception
date: 2020-07-20 09:58:40 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of re-throwing all but a specific exception type
time_to_live: 1800
category: vim
---



Example of re-throwing all but a specific exception type...


```vim
try
  s/foo/bar/
catch
  if v:exception !~ '^Vim\%((\a\+)\)\=:E486'
    throw v:exception
  endif
endtry
```


Above will re-throw exceptions that are **not** similar to...


```
Vim(substitute):E486: Pattern not found: foo
```
