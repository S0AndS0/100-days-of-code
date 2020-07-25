---
layout: post
title: Bash Date Calculations
date: 2020-04-27 21:08:27 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Hacking time within the Bash shell
time_to_live: 1800
category: bash
---



Calculating with Bash when #100DaysofCode is finished...


```bash
date -d "+100 days" +'%Y-%m-%d'
#> 2020-08-05
```


... Shell scripting languages such as Bash can be beautifully terse;


- `%Y` full four digit year

- `%m` zero-padded month, eg. `01`

- `%d` zero padded day, eg. `01`


Checkout `date --help` for full list of formatting syntax.


Till tomorrow here's one more example for going back in time...


```bash
date -d '-3 hour' +'%T'
#> 19:59:41
```
