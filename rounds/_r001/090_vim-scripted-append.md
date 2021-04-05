---
layout: post
title: Vim Scripted Append
date: 2021-04-04 17:25:00 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Another way of inserting text via Vim script
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://twitter.com/S0_And_S0/status/1378872242482872321
  title: Link to Tweet for this post
---



In a previous post I covered one method of using [Vim script to Insert Characters][link__100_days_of_code__r001_058__vim_script_insert_characters], while effective it has the drawback of using `execute` keyword.


The following however may be preferred by those, such as myself, that like keeping code _functional_...


```vim
call setline('.', getline('.') . repeat('*', 78))
```


For completeness here's a revision of previously published `insert_html_tag` function...


```vim
function! append_html_tag(name) abort
  let l:tag_text = '<' . a:name . '></' . a:name '>'
  setline('.', getline('.') . l:tag_text)
  let l:cursor_position = getpos('.')
  let l:cursor_position[1] -= length(a:name) + 3
  call setpos('.', l:cursor_position)
endfunction
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__100_days_of_code__r001_058__vim_script_insert_characters]: {{ r001/058_vim-script-insert-characters | relative_url }} "How to insert text with Ex mode commands"

