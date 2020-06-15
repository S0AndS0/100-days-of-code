---
layout: post
title: Awk `gsub` `FILENAME`
date: 2020-06-15 13:32:24 -0700
#date_updated:  # Optional and formatted like Mon Jun 15 13:32:24 PDT 2020 above
description: Example of using `gsub` function on `FILENAME` to count post languages
time_to_live: 1800
---



Example of using `gsub` function on `FILENAME` to count post languages...


```bash
awk '{
  if (FILENAME ~ "feed") { nextfile }
  path = FILENAME
  gsub( ".*([0-9]{3}_)|(-.*)", "", path)
  langs[path]++
  nextfile
}
END {
  for (key in langs) {
    print key, langs[key] | " sort"
  }
}' rounds/_r000/*
```


> Note, the `gsub()` function **cannot** be used directly on `FILENAME`


Example output...


```
awk 9
bash 15
css 1
git 2
html 1
javascript 16
nodejs 1
python 5
```
