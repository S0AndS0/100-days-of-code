---
layout: post
title: Bash STDOUT to Array
date: 2020-05-06 10:40:31 -0700
#date_updated:  # Optional and formatted like Wed May  6 10:40:31 PDT 2020 above
description: Saving output of a command to an array
time_to_live: 1800
---



Saving output of a command to an array in Bash...


```bash
_directory="/tmp/somewhere"

_stats=($(ls -ld "${_directory}" | awk '{ print $1, $3, $4; }'))


printf 'Permissions -> %s\n' "${_stats[0]}"
#> Permissions -> drwxrwxrwt
printf 'Group -> %s\n' "${_stats[1]}"
#> Group -> group
printf 'User -> %s\n' "${_stats[2]}"
#> User -> user
```


... additional parenthesis and lack of quotes surrounding sub-shell are the _magic sauce_, if instead quotes where included STDOUT would **not** be split by spaces into array elements...



```bash
_out=("$(ls -ld "/tmp/somewhere" | awk '{ print $1, $3, $4; }')")
printf 'Stats -> %s\n' "${_out[0]}"
#> Stats -> drwxrwxrwt group user
```


... in which case there'd be little point in assigning an array for a single command. However for collection of multiple results then double quotes do make a bit more sense...


```bash
_out+=("$(ls -ld "/tmp/elsewhere" | awk '{ print $1, $3, $4; }')")
printf '%s\n' "${_out[@]}"
#> drwxrwxrwt group user
#> drwxrwxrwt group user
```


___


## Attribution


- [AskUbuntu -- How to find owner and group of a directory](https://askubuntu.com/questions/175054/)
