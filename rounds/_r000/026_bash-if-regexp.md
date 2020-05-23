---
layout: post
title: Bash `if` RegExp
date: 2020-05-23 09:54:00 -0700
#date_updated:  # Optional and formatted like Sat May 23 09:54:00 PDT 2020 above
description: Example of Regular Expression branching/matching
time_to_live: 1800
---



Bash example script for Regular Expression branching/matching...


**`example.sh`**


```
#!/usr/bin/evn bash

_search="${1}"
_pattern="${2}"

[[ "${_search,,}" =~ ${_pattern} ]] || {
  printf >&2 'Did not find pattern -> %s\n' "${_pattern}"
  exit 2
}

printf 'Found pattern in -> %s\n' "${_search}"
```


Example usage...


```bash
bash example.sh "sorta Yep" '(yes|yep)$'
#> Found pattern in -> sorta Yep


bash example.sh "Not at all" '(yes|yep)$'
#> Did not find pattern -> (yes|yep)$
```


... the _magic sauce_ for matching is `=~` within _`if`_ test. Check [Bash Case Changing Built-ins]({{ '/r000/013-bash-case-changing-built-ins/' | relative_url }}) for more examples on `,,` usage.
