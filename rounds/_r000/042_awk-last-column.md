---
layout: post
title: Awk Last Column
date: 2020-06-08 11:04:37 -0700
#date_updated:  # Optional and formatted like Mon Jun  8 11:04:37 PDT 2020 above
description: Example of obtaining and using last column Awk variable
time_to_live: 1800
---



Example of obtaining last column of input


```bash
awk '{ print $NF }' <<'EOF'
Lorem ipsum sit
amet, adipisicing
sed do eiusmod tempor
EOF
#> sit
#> adipisicing
#> tempor
```


... This can be super useful when combined with FS (field separator) too, here's an example of _sanitizing_ a CSV to rows that contain the same number of columns as the heading...



```bash
awk -F, '{
  if (NR == 1) {
    table_last_column = NF
  } else if (table_last_column == NF) {
    print $0
  }
}' <<'EOF'
one,two,three,four
1,lamb,space,ham
2,spam,jam
3,fancy,blue,trousers
EOF
#> 1,lamb,space,ham
#> 3,fancy,blue,trousers
```
