---
layout: post
title: Awk float comparison hack for Bash
date: 2020-05-17 12:45:11 -0700
#date_updated:  # Optional and formatted like 'date' above
description: By default Bash does not support floating point number comparisons
time_to_live: 1800
category: awk
---




By default Bash does not support floating point number comparisons...


```bash
[[ '2.1' -gt '1.2' ]] && {
  printf 'true\n'
} || {
  printf 'false\n'
}
#> syntax error: invalid arithmetic operator (error token is ".1")


(('1.2' < '2.1')) && {
  printf 'true\n'
} || {
  printf 'false\n'
}
#> syntax error: invalid arithmetic operator (error token is ".2 < 2.1")
```


... however, with a bit of Awk redirection it is possible to add this functionality...


```bash
compare_floats() {
  awk 'BEGIN { if ('"$@"') { exit 0; } exit 1; }'
}
```


Example usage...


```bash
compare_floats '2.1 > 1.2' && {
  printf 'totally true\n'
} || {
  printf >&2 'oh so false\n'
}
#> totally true


if compare_floats '2.1 < 1.2'; then
  printf 'totally true\n'
else
  printf >&2 'oh so false\n'
fi
#> oh so false
```
