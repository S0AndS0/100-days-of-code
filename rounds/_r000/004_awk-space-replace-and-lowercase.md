---
layout: post
title: Awk Space Replace and Lowercase
date: 2020-05-01 09:28:14 -0700
#date_updated:  # Optional and formatted like 'date' above
description: String mutation Awk examples
time_to_live: 1800
category: awk
---


String mutation Awk examples


```bash
awk '{
  gsub(" ", "-", $0);
  print tolower($0);
}' <<<"Lamb SPAM haM"
#> lamb-spam-ham
```


**Syntax of `gsub(_match_, _replace_, _target_)`**


- _match_ can be a string (`"0"`), regular-expression (`/[0-9]/`), or variable

- _replace_ can be string, number, or variable

- _target_ can be input target, variable, or string


------


**`file.csv`**


```csv
name,hours,rate
Bill,38,4.7
Ted,40,5
```


```bash
awk 'FNR > 1 {
  gsub(",", " ", $0);
  print $1, "->", $2 * $3;
}' "file.csv"
#> Bill -> 178.6
#> Ted -> 200
```


> Note, in above example `gsub` is not necessarily necessary, and re-assigning the Field Separator may be better for CSV parsing...


```bash
awk 'BEGIN {
  FS = ","
}
{
  if (FNR > 1) {
    print $1, "->", $2 * $3;
  }
}' "file.csv"
#> Bill -> 178.6
#> Ted -> 200
```
