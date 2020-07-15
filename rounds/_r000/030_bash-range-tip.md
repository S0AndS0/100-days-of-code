---
layout: post
title: Bash range tip
date: 2020-05-27 14:44:54 -0700
#date_updated:  # Optional and formatted like 'date' above
description: The `{_start_.._end_}` syntax works in places other than `for` loops
time_to_live: 1800
---



The `{_start_.._end_}` syntax works within `for` loops...


```bash
for i in {0..2}; do
  printf '%i\n' "${i}"
done
#> 0
#> 1
#> 2
```


... but one thing to keep in mind is that ranges work with globing too...


```bash
ls ~/logs/apt_upgrade/20200{3..4}*
#> 20200301.script
#> 20200401.script
#> ...
```


... which can be useful for pre-filtering results within a pip-line.
