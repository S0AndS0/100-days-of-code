---
layout: post
title: Awk match between separator
date: 2020-07-10 16:42:58 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `index` and `substr` functions to extract between separator
time_to_live: 1800
category: awk
---



Example of using `index` and `substr` functions to extract between separator...


```bash
awk -v sep='"' '{
  i = index($0, sep)
  if (!i) { next; }
  s = substr($0, i + 1)
  i = index(s, sep)
  if (!i) { next; }
  s = substr(s, 0, i - 1)
  if (length(s)) { print s; }
}' <<'EOF'
ham "spam" can
EOF
#> spam
```


As a generalized Awk script...


**`match-between.awk`**


```awk
#!/usr/bin/awk -f


BEGIN {
  if (!sep) {
    print "No separator defined!"
    exit 1
  }
}

{
  i = index($0, sep)
  if (!i) {
    next
  }

  s = substr($0, i + 1)
  i = index(s, sep)
  if (!i) {
    next
  }

  s = substr(s, 0, i - 1)
  if (length(s)) {
    print s
  }
}
```


Example usage...


```bash
match-between.awk -v sep='"' <<'EOF'
ham flavored "spam"
EOF
#> spam
```
