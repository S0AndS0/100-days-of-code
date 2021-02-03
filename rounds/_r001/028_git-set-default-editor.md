---
layout: post
title: Git Set Default Editor
date: 2021-02-01 22:09:10 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to configure text editor that Git uses by default
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1356487164654141446
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How do I make Git use the editor of my choice for commits?
      href: https://stackoverflow.com/questions/2596805/
      title: How do I make Git use the editor of my choice for commits?
      class: fa fa-stack-overflow
---



Setting the default editor for Git is useful for writing multi-line commit messages from the command-line; following command will set Vim to the default editor for the currently logged-in account...


```bash
git config --global core.editor vim
```


> Note, remove the `--global` flag from above command to set for current responsory


Within a Git repository using `git commit` with no additional arguments will now open a Vim buffer.


- Press <kbd>i</kbd> to begin Insert mode

- Type message then press <kbd>Esc</kbd>

- Use Ex command `:wq`, or <kbd><kbd>Z</kbd><kbd>Z</kbd></kbd> keyboard shortcut within Normal mode to save and exit the buffer


For text editor that require parameters, such as Atom, use quotes to surround the editor and command-line options, eg...


```bash
git config core.editor 'atom --wait'
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

