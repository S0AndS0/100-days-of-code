---
layout: post
title: Bash read file lines
date: 2020-06-20 13:18:10 -0700
#date_updated:  # Optional and formatted like Sat Jun 20 13:18:10 PDT 2020 above
description: Example of reading lines from a file without the `cat` command
time_to_live: 1800
---



Example of reading lines from a file without the `cat` command...


```bash
while read -r _line; do
  printf '%s\n' "${_line}"
done <"directory/file.ext"
```


> Note, there's no need of `cat` command if `<` redirection is used instead.


Example of reading lines from command's Standard Out...


```bash
while read -r _line; do
  printf '%s\n' "${_line}"
done < <(ls "./")
```
