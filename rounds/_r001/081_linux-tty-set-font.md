---
layout: post
title: Linux TTY Set Font
date: 2021-03-26 19:37:14 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Couple of simple scripts I use for setting TTY font sizes
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



When I need a distraction free writing time I like to use TTY sessions, ie. no window-manager (GUI). However, the default font size after awhile can be a bit dense, and a wall of text can be nearly as disruptive to productivity.


The following two scripts are what I use for quickly adjusting font sizes within TTY sessions...


**`~/bin/22x11`**


```bash
#!/usr/bin/env bash

setfont '/usr/share/consolefonts/Uni3-TerminusBold22x11.psf.gz'
showconsolefont
```


**`~/bin/24x12`**


```bash
#!/usr/bin/env bash

setfont '/usr/share/consolefonts/Uni3-TerminusBold24x12.psf.gz'
showconsolefont
```


Using the keyboard shortcut <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>F5</kbd>, and <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>F6</kbd>, I can pop between a text-only interface and default window-managed GUI.


While in a TTY session running the above scripts is as easy as...


```bash
22x11
```


... or...


```bash
24x12
```


... to resize the current font.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

