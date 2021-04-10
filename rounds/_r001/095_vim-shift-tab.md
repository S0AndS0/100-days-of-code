---
layout: post
title: Vim Shift Tab
date: 2021-04-09 19:27:36 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to make <Tab> and <s-Tab> do smarter things
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- Map shift-tab in vim to inverse tab in Vim
      href: https://stackoverflow.com/questions/4766230/
      title: Map shift-tab in vim to inverse tab in Vim
      class: fa fa-stack-overflow

    - text: Vi StackExchange -- Cycle through autocomplete menu using tab
      href: https://vi.stackexchange.com/questions/19675/
      title: Cycle through autocomplete menu using tab
      class: fa fa-stack-exchange
---



Today I invested much of the day towards documenting my Vim configurations in preparation for publishing next week. And because of this preparation I debugged one group of mappings that I've been partially using for the `<tab>`


**`~/.vimrc` (snip)**


```vim
inoremap <expr> <Tab> pumvisible() ? "\<C-n>" : "\<Tab>"
inoremap <expr> <s-Tab> pumvisible() ? "\<C-p>" : "\<C-d>"

nnoremap <Tab> >>
nnoremap <S-Tab> <<

vnoremap <Tab> >gv
vnoremap <S-Tab> <gv
```


**Insert Mode**


The `pumvisible()` function will return `1` if the preview/auto-complete menu is shown and `0` otherwise, this allows <kbd>Tab<kbd>, and <kbd>Shift<kbd> <kbd>Tab<kbd>, keys to either cycle through menu options or insert/remove indentation.


> Note, within Normal mode for some reason `<s-Tab>` functioned more reliably than `<S-Tab>`


**Normal Mode**


The `>>`, and `<<`, key sequences are by default adjust indentation.


**Visual Mode**


By default the `>`, and `<`, key sequences will exit back to Normal mode after adjusting indentation, using the `gv` command will automatically re-select the previously selected lines, which resumes Visual mode.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

