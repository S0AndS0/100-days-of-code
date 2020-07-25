---
layout: post
title: Awk Floating Point Calculator
date: 2020-05-11 08:56:30 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Dependency free floating point math from the command-line
time_to_live: 1800
category: awk
---



Dependency free floating point math from the command-line


**`calc.sh`**


```bash
#!/usr/bin/env bash

calc() {
  awk 'BEGIN { print '"${@//inf/(2 ** 1024)}"'; }'
}

calc '1/2'
#> 0.5
```


------


Alternatively, the above may be expressed as an Awk script for parsing file like inputs...


**`calc.awk`**


```awk
#!/usr/bin/awk -f

function calc(expression) {
  gsub("inf", "(2 ** 1024)", expression)
  system(sprintf("awk \"BEGIN {printf(" expression ")}\""))
}

{
  print calc($0)
}
```


> Note, `calc` function uses `printf` to suppress new lines, enabling _cleaner_ redirection of output


## Example `calc.awk` usages


Single line...


```bash
calc.awk <<<'(3+4)/5'
#> 1.4

printf '(5+4)/3' | calc.awk
#> 3
```


Multiple lines...


```bash
calc.awk <<'EOF'
(3 + 4) / 5
(5 + 4) / 3
EOF
#> 1.4
#> 3
```


File input(s)...


```bash
calc.awk file.one file.two
```


## Attribution


- [StackOverflow -- evaluate arithmetic expression passed as argument in awk](https://stackoverflow.com/a/46511043)

- [Twitter -- `inf` explanation from @DracoMetallium](https://twitter.com/DracoMetallium/status/1260939962477948932)
