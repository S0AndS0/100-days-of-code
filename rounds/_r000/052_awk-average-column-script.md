---
layout: post
title: Awk average column script
date: 2020-06-18 10:18:04 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using ternary operator to default undefined variables
time_to_live: 1800
---



Example of using ternary operator to default undefined variables...


**`average.awk`**


```awk
#!/usr/bin/awk -f

BEGIN {
  column = column? column: 1
}

{
  if ($column || $column == 0) {
    count++
    total += $column
  }
}

END {
  print total / count
}
```


Example usage...


```bash
average.awk column=2 <<EOF
1 2
3 4
5 6
-1 -2
EOF
#> 2.5
```
