---
layout: post
title: Vim Performance Profiling
date: 2021-04-13 17:13:56 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to find features and/or code that are slowing Vim down
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1382125732739043332
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How to see which plugins are making Vim slow?
      href: https://stackoverflow.com/questions/12213597/
      title: How to see which plugins are making Vim slow?
      class: fa fa-stack-overflow

    - text: StackOverflow -- Vim slows down over time with syntax on
      href: https://vi.stackexchange.com/questions/2875/
      title: Vim slows down over time with syntax on
      class: fa fa-stack-overflow
---



As powerful as Vim is there are some limitations, and occasionally when writing plugins or other customizations it is possible to develop bugs instead of solutions.


The following sequence of Vim Ex mode commands are able to profile time spent on syntax highlighting...


```Vim
syntax off
syntime on
syntax on

" ... Scroll about for a bit...

syntime report
```


And the next set of Ex mode commands are very helpful in profiling time spent executing Vim functions and scripts...


```Vim
profile start /tmp/vim-profile.log
profile func *
profile file *

" ... preform actions...

profile pause
noautocmd qall!
```


On occasion either of above may produce more output than is necessary, or convenient to parse, in such cases it may be helpful to start Vim without any configurations...


```bash
vim -u NONE /tmp/test.txt
```


... then set, or source, configurations and/or scripts, eg...


```vim
source ~/.vimrc.d/plugged/00-init.vim
source ~/.vimrc.d/plugged/gruvbox.vim
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

