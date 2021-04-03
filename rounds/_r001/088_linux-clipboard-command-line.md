---
layout: post
title: Linux Clipboard Command Line
date: 2021-04-02 16:53:47 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Tips and tricks for interacting with Linux clipboard via command-line
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://twitter.com/S0_And_S0/status/1378134904425353224
  title: Link to Tweet for this post
---



I'm constantly discovering new reasons to like Linux, today I researched a bit on how to enteract with the X11 clipboard via command line and found an excellent tool `xclip` that does precisely what I wanted.


Here's a few quick, and explicit, examples of usage


Print content of `clipboard` selection to STOUT (Standard Out)


```bash
xclip -selection clipboard -out
```


Write `foo` to `clipboard` selection


```bash
xclip -selection clipboard -in <<<'foo'
```


Check the manual for more details


```bash
man xclip
```


The first, of many, use-cases I've found `xclip` useful for is copying the last run command into the clipboard, eg...


```bash
man --pager='less --pattern="^\s+-selection"' xclip

 xclip -in < <(printf '%s' "!!")
```


... by using `!!` trick and a bit of input/output redirection the previous command is injected into my clipboard, and ready for pasting elsewhere!


> Note, above `xclip` command may be further shortened to ` xclip -in <<<"!!"`


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

