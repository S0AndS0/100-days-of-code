---
layout: post
title: Awk argument parsing
date: 2020-05-29 11:05:54 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of parsing arguments within Awk script
time_to_live: 1800
---



Example of parsing arguments within Awk script...


**`hello-args.awk`**


```awk
#!/usr/bin/awk -f

BEGIN {
  _name = "world"

  for (i = 1; i < ARGC; i++) {
    if (ARGV[i] ~ "^--name=") {
      _name = substr(ARGV[i], 8)
      delete ARGV[i]
    }
  }

  print "Hello", _name "!"
}
```


Add executable permissions...


```bash
chmod u+x hello-args.awk
```


Then send _`--name="_string_"`_ to script...


```bash
hello-args.awk --name='spam'
#> Hello spam!
```


> Note, the _`delete ARGV[i]`_ bit is required to prevent Awk from treating matched sequence as standard input.
