---
layout: post
title: Bash string splitting trick
date: 2020-06-25 12:09:56 -0700
#date_updated:  # Optional and formatted like Thu Jun 25 12:09:56 PDT 2020 above
description: Example of using find and replace Bash built-ins on variables
time_to_live: 1800
---



Example of using find and replace Bash built-ins on variables...


```bash
_string='spam:flavored:ham'

for _word in ${_string//:/ }; do
  printf '%s\n' "${_word}"
done
#> spam
#> flavored
#> ham
```


... the _magic sauce_ is _`//<find>/<replace>`_ syntax on variables.
