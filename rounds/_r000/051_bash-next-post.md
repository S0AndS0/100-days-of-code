---
layout: post
title: Bash next post
date: 2020-06-17 10:36:05 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Function that prints the index for new post file
time_to_live: 1800
---



Function that prints the index for new post file...


```bash
next_post_index(){
  local _list="$(ls -1 "${1}"/*.md 2>/dev/null)"
  local _index='0'
  (( ${#_list} )) && {
    _index="$(wc -l <<<"${_list}")"
  }
  printf '%03d\n' "${_index}"
}
```


Example usage...


```bash
next_post_index "rounds/_r000"
#> 051
```
