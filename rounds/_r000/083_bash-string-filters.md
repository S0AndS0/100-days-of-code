---
layout: post
title: Bash string filters
date: 2020-07-19 10:58:34 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Examples of using Bash built-ins for filtering before or after a pattern
time_to_live: 1800
category: bash
---



Examples of using Bash built-ins for filtering before or after a pattern...


```bash
string='spam flavored ham'


printf '%s\n' "${string%% *}"
#> spam

printf '%s\n' "${string##* }"
#> ham
```


... The _`%% *`_ bit will greedily remove everything after the first space, and the _`##* `_ bit greedily removes everything up-to last space.
