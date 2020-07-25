---
layout: post
title: Awk Sorted Unique Count
date: 2020-06-11 11:02:47 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Using an Awk array (map) to sort and count unique lines or columns
time_to_live: 1800
category: awk
---



Example of using an Awk array (map) to sort and count unique lines or columns


**`bin/sorted-unique-count.awk`**


```awk
#!/usr/bin/awk -f

{
  if ($column) {
    a[$column]++
  } else if (empty_key) {
    a[empty_key]++
  }
}

END {
  for (i in a) {
    if (i == empty_key) {
      print a[i] | " sort"
    } else {
      print a[i], i | " sort"
    }
  }
}
```


**Example usage**


```bash
bin/sorted-unique-count.awk column=1 <<'EOF'
asdf jkl
qwer jkl
asdf uio
zxcv uio
EOF
#> 1 qwer
#> 1 zxcv
#> 2 asdf


bin/sorted-unique-count.awk column=2 <<'EOF'
asdf jkl
qwer jkl
asdf uio
zxcv uio
EOF
#> 2 jkl
#> 2 uio
```
