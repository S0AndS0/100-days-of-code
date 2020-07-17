---
layout: post
title: Awk average select columns
date: 2020-07-17 12:18:26 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of Awk column selection by variable
time_to_live: 1800
---



Example of Awk column selection by variable...


**`average-columns.awk`**


```awk
#!/usr/bin/awk -f

function average_row_columns(from, till) {
  sum = 0
  for (i = from; i <= till; i++) {
    sum += $i
  }
  return sum / (1 + till - from)
}


BEGIN {
  from = from? from: 1
}

{
  till = till? till: NF
  print average_row_columns(from, till)
}
```


Usage example, average from column 4 till last column...


```bash
average-columns.awk from='4' <<'EOF'
1 2 3 4 5 6 7
9 8 7 6 5 4 3
EOF
#> 5.5
#> 4.5
```


Usage example, average all columns...


```bash
average-columns.awk <<'EOF'
1 2 3 4 5 6 7
9 8 7 6 5 4 3
EOF
#> 5.5
#> 4.5
```


Setting the Field Separator (`FS`) variable it is possible to parse CSV like inputs...


```bash
average-columns.awk FS=',' <<'EOF'
1.2,3.4,5.6
7.8,9.1,2.3
EOF
#> 3.4
#> 6.4
```
