---
layout: post
title: Bash Divide By Zero Gotcha
date: 2020-05-14 11:41:39 -0700
#date_updated:  # Optional and formatted like Thu May 14 11:41:39 PDT 2020 above
description: '`local` prevents trapping errors'
time_to_live: 1800
---



There are plenty of error codes that can be trapped on, however, divide by zero is supper tricky and using `local` prevents at least one known workaround from tripping traps...


**`trapping-divide-by-zero.sh`**


```bash
#!/usr/bin/env bash

set -E -o functrace

trap_callback() {
  _command="$1"
  _exit_code="${2:-0}"
  printf "%i -> %s\n" "${_exit_code}" "${_command}"
  exit "${_exit_code}"
}

trap 'trap_callback "$BASH_COMMAND" "$?"' ERR


bad_math() {
 local _results="$( $((1 / ${1})) || exit $? )"
 printf '%i\n' "${_results}"
}

ehh_math() {
 _results="$( $((1 / ${1})) || exit $? )"
 printf '%i\n' "${_results}"
}


bad_math 0
echo 'Uh-oh'
#> bash: 1 / 0: division by 0 (error token is "0")
#> Uh-oh


ehh_math 0
echo 'This wont show'
#> bash: 1 / 0: division by 0 (error token is "0")
#> 1 -> _results="$( $((1 / ${1})) || exit $? )"
```


## Attribution


- [Unix StackExchange -- Ignore or catch division by zero](https://unix.stackexchange.com/questions/28016/)
