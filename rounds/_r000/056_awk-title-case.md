---
layout: post
title: Awk title case
date: 2020-06-22 10:04:28 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example script that title cases all words in string
time_to_live: 1800
---



Awk script that title cases all words in string...


**`title-case.awk`**


```awk
#!/usr/bin/awk -f


function join(array, separator, _result) {
  for (i = 0; i < length(array); i++ ) {
    if (_result) {
      _result = _result separator array[i]
    } else {
      _result = array[i]
    }
  }
  return _result
}

function titleCase(string) {
  split(string, array, " ")
  for (i = 0; i < length(array); i++) {
    array[i] = toupper(substr(array[i], 1, 1)) substr(array[i], 2, length(array[i]))
  }
  return join(array, " ")
}


{
  print titleCase($0)
}
```


Example usage...


```bash
title-case.awk <<<'jayne cobb'
#> Jayne Cobb


title-case.awk <<'EOF'
Lorem ipsum dolor
sit amet, consectetur
adipisicing elit, sed
EOF
#> Lorem Ipsum Dolor
#> Sit Amet, Consectetur
#> Adipisicing Elit, Sed
```
