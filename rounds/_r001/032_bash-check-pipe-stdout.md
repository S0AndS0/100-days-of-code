---
layout: post
title: Bash Check Pipe STDOUT
date: 2021-02-05 18:14:10 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to check if Bash script output is piped
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Recently for one of my Bash related projects that colorized output, I had the need to check if script output was redirected to a pipe; in such cases said script had to produce output without escape codes that colorize output.


Here's an example script that demonstrates checking for _`STDOUT`_ piping...


**`pipe-check.sh`**


```bash
#!/usr/bin/env bash


if [[ -t 1 ]]; then
    printf 'Standard out is terminal\n'
else
    printf >&2 'Standard out is not terminal!?\n'
fi
```


**Usage Examples**


```bash
./pipe-check.sh
#> Standard out is terminal

./pipe-check.sh | cat -
#> Standard out is not terminal!?
```


Use the following incantation to jump to relevant manual section...


```bash
man --pager="less -p '^[[:space:]]+-t'" bash
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

