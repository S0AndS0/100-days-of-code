---
layout: post
title: Vim Glob
date: 2021-03-29 17:57:07 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Using glob function to source vim configurations from sub-directories
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1376701350537482245
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How to source all vim files in directory
      href: https://stackoverflow.com/questions/4500748/66847890#66847890
      title: How to source all vim files in directory
      class: fa fa-stack-overflow
---



I've been methodically organizing my Vim configurations such that they may be published for others to utilize. The following Vim function is what I've written to enable loading configuration files from a sub-directory...


**`~/.vimrc` (snip)**


```vim
""
" Executes source on Vim configuration files within '.vimrc.d' directory
function! Load_Vim_Configs_From_Directories() abort
  let l:script_directory = fnamemodify(expand('<sfile>'), ':p:h')
  let l:glob_pattern = l:script_directory . '/.vimrc.d/**/*.vim'

  for l:f in glob(l:glob_pattern, 1, 1)
    execute 'source' l:f
  endfor
endfunction

call Load_Vim_Configs_From_Directories()
```


... with that one bit, I'm now able to organize configurations similar to...


```
~/.vimrc.d/
    balanced-backspace.vim
    balanced-braces.vim
    balanced-quotes.vim
    markdown.vim
    netrw.vim

    plugged/
        00-init.vim
        emmet.vim
        gruvbox.vim
        syntastic.vim
        you-complete-me.vim

    set.vim
```


---


Check `vim -c ':help glob'` for details about additional `glob` arguments.


**TLDR**


```
glob({expr} [, {nosuf} [, {list} [, {alllinks}]]])
```

- _`{expr}`_ may be a string with wildcards _(`*`)_ or a command (wrapped in backticks) that evaluates to a string

- _`{nosuf}`_ set to _False_ allows 'suffixes' and 'wildignore' options to apply

- _`{list}`_ set to _True_ causes `glob` to return a list that respects new-lines within file names


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

