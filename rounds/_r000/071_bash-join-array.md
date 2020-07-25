---
layout: post
title: Bash join array
date: 2020-07-07 12:40:44 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Function to join Bash array/list
time_to_live: 1800
category: bash
---



Function to join Bash array/list...


```bash
array_join() {
  local -n _array="${1:?No array reference provided}"
  local _separator="${2:-,}"
  printf '%s\n' "$(IFS=${_separator}; printf '%s' "${_array[*]}")"
}
```


Example usage...


```bash
list_one=(spam flavored ham)
array_join list_one
#> spam,flavored,ham


list_two=('spaced string' 'something else')
array_join list_two '-'
#> spaced string-something else
```


## Attribution
[heading__attribution]: #Attribution


- [CommandLineFu -- Join the content of a bash array with commas](https://www.commandlinefu.com/commands/view/12759/join-the-content-of-a-bash-array-with-commas)
