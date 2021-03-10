---
layout: post
title: Vim Type Comparisons
date: 2021-03-09 16:30:41 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to check type of variable within Vim script
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Some of the Vim plugins that I maintain allow variables to have different types, for example the [`vim-utilities/balanced-quotes`][link__github__vim_utilities__balanced_quotes] project allows for a file path (string), or dictionary, for configuring plugin behaviour.


As of Vim version `8.2` documentation from `:help type()` states there are eleven (11) data types, of which eight (8) are relatively easy to inspect via `type()` function...


```vim
#!/usr/bin/env vim


function! print_type(variable) abort
  if type(a:variable) == type(0)
    echomsg "Number"
  elseif type(a:variable) == type("")
    echomsg "String"
  elseif type(a:variable) == type(function("tr"))
    echomsg "Function"
  elseif type(a:variable) == type([])
    echomsg "List"
  elseif type(a:variable) == type({})
    echomsg "Dictionary"
  elseif type(a:variable) == type(0.0)
    echomsg "Float"
  elseif type(a:variable) == type(v:false)
    echomsg "Boolean"
  elseif type(a:variable) == type(v:none)
    echomsg "None"
  else
    echomsg "Type ->" . type(a:variable)
  endif
endfunction


call print_type(42)
"> Number
call print_type(4.2)
"> Float
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__github__vim_utilities__balanced_quotes]: https://github.com/vim-utilities/balanced-quotes

