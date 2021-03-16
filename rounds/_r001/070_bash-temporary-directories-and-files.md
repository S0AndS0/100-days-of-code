---
layout: post
title: Bash Temporary Directories and Files
date: 2021-03-15 21:40:08 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Quick how to on generating temporary directory/file within Bash scripts
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



While preparing a new project for publishing I had need of _caching_ data to a file-system.


Fortunately there be magics of `mktemp` command, which is able to make temporary files and/or directories, eg...


```bash
_tmp_directory="$(mktemp --directory)"

_tmp_file="$(mktemp --tmpdir="${_tmp_directory}")"


printf '_tmp_directory -> %s\n' "${_tmp_directory}"
#> _tmp_directory -> /tmp/tmp.pHKQ0inpWM

printf '_tmp_file      -> %s\n' "${_tmp_file}"
#> _tmp_file      -> /tmp/tmp.pHKQ0inpWM/tmp.r0UCPUgC8E
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

