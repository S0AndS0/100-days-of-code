---
layout: post
title: Bash `select` options
date: 2020-07-28 11:42:44 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `select` from list of options
time_to_live: 1800
---



Example of using `select` from list of options...


**`select-example.sh`**


```bash
#!/usr/bin/env bash

chosen=()
choices=(spam ham salad)

PS3='Select dinners: '
select dinner in ${choices[@]}; do
  ((${#dinner})) || { break; }
  chosen+=($dinner)
done

printf '%s\n' "${chosen[@]}"
```


Example usage


```bash
select-example.sh
#< 1
#< 3
#< 0

#> spam
#> salad
```

