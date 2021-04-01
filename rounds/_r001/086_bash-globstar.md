---
layout: post
title: Bash globstar
date: 2021-03-31 15:50:24 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Examples of using shopt to extend globing features of Bash
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://twitter.com/S0_And_S0/status/1377394703377793026
  title: Link to Tweet for this post
---



Few days ago I wrote about [Vim `glob`][link__100_days_of_code__r001_084__vim_glob] function and thought the `dir/**/*.ext` syntax would be swell if it where supported by Bash, because most of my use cases for the `find` command would be covered. At first it didn't seem likely, however, after a quick search through the manual pages I found the `globstar` option.


Here's a _short-cut_ for jumping to the relevant manual section...


```bash
man --pager='less --pattern="^\s+globstar"' bash
```


... And a quick command on how to check if the option is already set...


```bash
shopt -u | grep globstar
#> shopt -u globstar
```


Effectively the `**/*` syntax will search the current directory **and** sub-directories for matches.


Here's a quick example script for finding files of a specific extension...


**`ext-search.sh`**


```bash
#!/usr/bin/env bash

shopt -s globstar


_ext="${1?No file extention provided}"
_dir="${2:-${PWD}}"


for _path in "${_dir}"/**/*."${_ext}"; do
  printf '%s\n' "${_path}"
done
```


... and a quick example usage...


```bash
ext-search.sh 'txt' 'some/directory'
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__100_days_of_code__r001_084__vim_glob]: {{ r001/084-vim-glob | absolute_url }} "Using glob function to source vim configurations from sub-directories"

