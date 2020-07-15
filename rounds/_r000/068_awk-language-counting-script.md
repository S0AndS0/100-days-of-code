---
layout: post
title: Awk language counting script
date: 2020-07-04 11:56:24 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using Awk to print statistics about posts published
time_to_live: 1800
---



Example of using Awk to print statistics about posts published...


**language-counter.awk**


```awk
#!/usr/bin/awk -f

BEGIN {
  delete ignore_list
  if (ignore) {
    split(ignore, a, ",")
    for (k in a) {
      ignore_list[a[k]]++
    }
  }
}

{
  if (FILENAME !~ ".md$") { nextfile; }
  path = FILENAME
  gsub(".*[0-9]{3}_", "", path)
  split(path, lang, "-")
  if (lang[1] in ignore_list) { nextfile; }
  counts[lang[1]]++
  nextfile
}

END {
  for (k in counts) {
    print counts[k], k | " sort -n"
  }
}
```


Example usage...


```bash
./language-counter.awk -v ignore='three' rounds/_r000/*
```


Example output...


```
1 css
1 html5
1 nodejs
2 git
3 html
7 python
14 awk
18 bash
20 javascript
```
