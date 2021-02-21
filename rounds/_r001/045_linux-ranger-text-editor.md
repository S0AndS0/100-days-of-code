---
layout: post
title: Linux Ranger Text Editor
date: 2021-02-18 17:55:43 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to configure Ranger file manager default text editor
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1362655176667062282
  title: Link to Tweet for this post

attribution:
  links:
    - text: Unix StackExchange -- How to change the default text editor in ranger?
      href: https://unix.stackexchange.com/questions/367452/
      title: How to change the default text editor in ranger?
      class: fa fa-stack-exchange
---



Ranger is a terminal based file manager with some excellent features, such as bulk renaming, and Vim like key bindings. This post is a _crash course_ for installing, configuring the default text editor, and bulk renaming selected paths.


Install via package manager...


```bash
sudo apt-get update

sudo apt-get install ranger
```


Copy the `rifle.conf` file from `/etc/ranger/config` directory via...


```bash
ranger --copy-config=rifle
```


Edit account specific `rifle.conf` file to enable using Vim as the default text editor.


```bash
vim ~/.config/ranger/rifle.conf
```


**`~/.config/ranger/rifle.conf` (snip)**


```
#-------------------------------------------
# Misc
#-------------------------------------------
# Define the "editor" for text files as first action
mime ^text,  label editor = vim -- "$@"
# mime ^text,  label editor = $EDITOR -- "$@"
```


Start ranger with `some/directory` path...


```bash
ranger some/directory
```


Start visual selection via <kbd>Shift</kbd> <kbd>V</kbd> keyboard shortcut, and using <kbd>j</kbd> or <kbd>k</kbd> keys to add to selection.


Then enter the following Ex mode _like_ command to open a buffer with selected paths for renaming...


```ranger
:bulkrename
```

______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

