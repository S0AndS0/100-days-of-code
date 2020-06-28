---
layout: post
title: Awk builtin linter
date: 2020-06-28 11:08:36 -0700
#date_updated:  # Optional and formatted like Sun Jun 28 11:08:36 PDT 2020 above
description: Examples of using the builtin linter within Awk from GNU
time_to_live: 1800
---



Examples of using the builtin linter within Awk from GNU...


```bash
awk --lint-old '{
  while ( (getline _line < $0) > 0) {
    print _line
  }
  close($0)
}' <<<'file.ext'
#> awk: cmd. line:2: warning: `getline' is not supported in old awk
#> awk: cmd. line:5: warning: `close' is not supported in old awk
```


These command-line parameters also work with Awk scripts...


**`cat.awk`**


```awk
#!/usr/bin/awk -f

{
  while ( (getline _line < $0) > 0) {
    print _line
  }
  close($0)
}
```


Example usage...


```bash
cat.awk --lint-old 'file.ext'
```


... there's also `--lint=fatal` and `-L invalid` options for more linting goodness.
