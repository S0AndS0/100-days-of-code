---
layout: post
title: Awk calling shell executable
date: 2020-05-25 11:19:06 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of calling `ls` and reading STDOUT within Awk script
time_to_live: 1800
category: awk
---



Example of calling `ls` and reading STDOUT within Awk script...


**`list-test.awk`**


```awk
#!/usr/bin/awk -f

BEGIN {
  _path = "~/"
  cmd = "ls " _path
  while ( (cmd | getline _line) > 0) {
    print _path _line
  }
  close(cmd)
}
```


Example usage...


```bash
./list-test.awk
#> ~/bin
#> ~/Desktop
#> ~/Documents
#> ~/Downloads
#> ...
```


> Note, the `close(cmd)` is a really good idea, especially for more complex scripts.
