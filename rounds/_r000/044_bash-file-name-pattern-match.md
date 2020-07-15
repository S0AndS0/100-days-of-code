---
layout: post
title: Bash File Name Pattern Match
date: 2020-06-10 10:47:22 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of extracting a file name with Pattern Match built-ins within Bash
time_to_live: 1800
---



Example of extracting a file name with Pattern Match built-ins within Bash


```bash
_file_path='some/where/file.ext'

_file_name="${_file_path//*(*\/|.*)/}"

printf 'File name -> %s\n' "${_file_name}"
#> File name -> file
```


... the _magic sauce_ is `*()` and `|` to match one or more listed patterns.


## [#][heading__attribution] Attribution
[heading__attribution]: #attribution


- [GNU Manual -- 3.5.8.1 Pattern Matching](https://www.gnu.org/software/bash/manual/html_node/Pattern-Matching.html)
