---
layout: post
title: Bash Padding Strings
date: 2020-04-28 10:47:52 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Pad string in Bash with zeros
time_to_live: 1800
category: bash
---



Pad string in Bash with zeros...


```bash
printf '%03d\n' "1"
#> 001


printf '%03d\n' "12"
#> 012
```


... such options are often available within other languages too...


```bash
awk '{ printf("%03d\n", $1); }' <<<"3"
#> 003
```
