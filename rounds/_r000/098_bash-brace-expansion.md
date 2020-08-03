---
layout: post
title: Bash brace expansion
date: 2020-08-03 14:50:45 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Examples of using Bash brace expansion for command-line operations
time_to_live: 1800
---


Examples of using Bash brace expansion for command-line operations...


```bash
ls rounds/_r000/0{40..45}*
#> rounds/_r000/040_bash-pattern-matching.md
#> rounds/_r000/041_javascript-ternary-operator.md
# ...
```


The `..` syntax within curly-braces is a Bash way of defining a range, and using `,` within curly-braces instead is a way of defining a set within Bash...


```bash
mkdir /tmp/test_{one,two,three}

ls /tmp/test_*
#> /tmp/test_one
#> /tmp/test_two
#> /tmp/test_three
```
