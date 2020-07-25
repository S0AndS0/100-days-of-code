---
layout: post
title: Bash Error Trapping
date: 2020-05-12 09:09:49 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of catching/inspecting Bash error states
time_to_live: 1800
category: bash
---




Example of catching/inspecting Bash error states...


**`simple-trap.sh`**


```bash
#!/usr/bin/env bash

trap_callback() {
  printf >&2 '%i -> %s\n' "${2}" "${1}"
  exit "${2}"
}

trap 'trap_callback "${BASH_COMMAND}" "${?}"' ERR

bogus-command --parameter spam
```


```bash
bash simple-trap.sh
#> 127 -> bogus-command --parameter spam
```
