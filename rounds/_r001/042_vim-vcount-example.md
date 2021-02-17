---
layout: post
title: Vim `v:count` Example
date: 2021-02-15 20:07:23 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `v:count` builtin variable
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1361530015716900867
  title: Link to Tweet for this post

attribution:
  links:
    - text: Make mapping that accepts count independent of line count
      href: https://vi.stackexchange.com/questions/21485/
      title: Make mapping that accepts count independent of line count
      class: fa fa-stack-exchange
---


When writing Vim plugins there are instances when allowing a count prefix for some key sequence would be useful. For example _`2hl`_ the _`hl`_ would be the expression, and _`2`_ would be an optional count.


This post will cover a quick example Vim plugin/template that may be extended.


First create the necessary directory/file structure...


```bash
mkdir -p ~/git/hub/vim-utilities

git init ~/git/hub/vim-utilities/example-v:count

cd ~/git/hub/vim-utilities/example-v:count

mkdir plugin

touch plugin/example-v:count.vim
```


Then write the following file...


**`plugin/example-v:count.vim`**


```vim
#!/usr/bin/env vim


""
" @see {docs} - help v:count
" @see {docs} - help echohl
" @see {docs} - help :highlight
" @see {docs} - help :map-<expr>
function! Debug_Expr(...) abort
  echohl ErrorMsg
  echomsg 'a:000 ->' join(a:000)
  echohl Normal
endfunction


""
" Bind <count>F4 to Debug_Expr() function
nnoremap <F4> :<C-U>call Debug_Expr(v:count)<CR>
```


Finally `source` the plugin script within a Vim session...


```vim
:source ~/git/hub/vim-utilities/example-v\:count/plugin/example-v\:count.vim
```


Now typing a number prior to pressing <kbd>F4</kbd> _should_ produce some debug output, eg...


- <kbd>F4</kbd> -> `a:000 -> 0`

- <kbd>5</kbd> <kbd>F4</kbd> -> `a:000 -> 5`


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__previous_post]: {{ 'r001/040-linux-image-conversion' | abosolute_url }} "Link to post about image format conversion"

