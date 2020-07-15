---
layout: post
title: Bash Case Changing Built-ins
date: 2020-05-10 09:16:32 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Lower or upper case strings with Bash built-ins
time_to_live: 1800
---



Change lower/upper casing for all characters within a string...


```bash
yell() { printf '%s\n' "${@^^}"; }

whisper() { printf '%s\n' "${@,,}"; }

yell 'ham'
#> HAM
whisper 'SPAM'
#> spam
```


Capitalize first letter of each word in a space separated list of words...


```bash
nouns() {
  local words=($@)
  printf '%s\n' "${words[*]^}"
}

nouns 'fancy' 'title'
#> Fancy Title
```
