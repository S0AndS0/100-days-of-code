---
layout: post
title: Awk RegExp variable
date: 2020-05-22 13:09:16 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of matching Regular Expression defined by variable
time_to_live: 1800
---



Example of matching Regular Expression defined by variable...


```bash
awk -v _pattern='(yep|yes)$' '{
  if (tolower($0) ~ _pattern) {
    print $0;
  }
}' <<'EOF'
yes sorta
maybe Yep
nope
EOF
#> maybe Yep
```


... hint, `~` is the _magic sauce_ for using RegExp defined within variables.
