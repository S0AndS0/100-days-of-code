---
layout: post
title: Awk array sorting
date: 2020-07-26 11:38:48 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using Awk built-ins for sorting columns
time_to_live: 1800
---



Example of using Awk built-ins for sorting columns...


**`column-sort.awk`**


```awk
#!/usr/bin/awk -f


BEGIN {
  separator = separator? separator: " "
  joiner = joiner? joiner: separator
}


{
  split($0, array, separator)
  asort(array, sorted)
  for (i = 1; i <= length(sorted); i++) {
    if (i == length(sorted)) {
      print sorted[i]
    } else {
      printf("%s%s", sorted[i], joiner)
    }
  }
}
```


Example usage...


```bash
column-sort.awk <<'EOF'
spam ham
lamb canned
EOF
#> ham spam
#> canned lamb
```
