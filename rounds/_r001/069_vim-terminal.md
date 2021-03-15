---
layout: post
title: Vim Terminal
date: 2021-03-14 16:59:28 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Quick tips on using terminal within Vim session
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Vim has many builtin features that I consider to be useful, one of which is the option to start a terminal session via Ex mode command within a split or tab, eg...


```vim
:terminal
```


... by default above will make a new horizontal split, initialize a new terminal session, and start Insert mode.


This behaviour may be customized by prefixing `vertical`...


```vim
:vertical terminal
```


Or a new Vim tab may be dedicated to the terminal session via...


```vim
:tab terminal
```


Defining a shell environment or script is also possible, for example the following will start NodeJS terminal session within a new horizontal split...



```vim
:terminal node
```


Because the terminal session is within a Vim buffer, by using <kbd>Ctrl</kbd>^<kbd>w</kbd> prefix, it is possible to Yank and/or Put from/to other buffers.


Few keyboard shortcuts I use often


- `<c-w> <c-{h,j,k,l}>` Jumps to left (`h`), lower (`j`), upper (`k`), or right (`l`) buffer

- `<c-w> <c-{H,J,K,L}>` Moves or rotates splits, for example if terminal is horizontal <kbd>Ctrl</kbd>-<kbd>w</kbd> <kbd>Ctrl</kbd>-<kbd>H</kbd> will switch to a vertical layout and <kbd>Ctrl</kbd>-<kbd>w</kbd> <kbd>Ctrl</kbd>-<kbd>J</kbd> will switch back to horizontal layout

- `<c-w> <c-n>` (AKA <kbd>Ctrl</kbd>-<kbd>w</kbd> <kbd>Ctrl</kbd>-<kbd>c</kbd>) Switches to Normal mode
  - <kbd>i</kbd> will switch bach to Insert mode
  - <kbd>v</kbd>, <kbd>V</kbd>, and `<c-v>` (AKA <kbd>Ctrl</kbd>-<kbd>v</kbd>) will switch to Visual selection modes
  - `/` and `?` will start searching terminal buffer

> Note, while in Normal mode most of the movement keys will function as expected

- `<c-w> <c-c>` (AKA <kbd>Ctrl</kbd>-<kbd>w</kbd> <kbd>Ctrl</kbd>-<kbd>c</kbd>) will terminate terminal session

- `<c-w> :` (AKA <kbd>Ctrl</kbd>-<kbd>w</kbd> <kbd>:</kbd>) will start Ex mode


Vim documentation has much more about usage and customization...


```vim
:help terminal
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

