---
layout: post
title: Vim Script Insert Characters
date: 2021-03-03 18:14:14 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to insert text with Ex mode commands
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



While writing various projects I occasionally have need to build formatted strings. For example when _sketching-out_ a script I like to clearly divide sections, eg...


```
#======================================#
```


Thankfully Vim makes such tasks relatively easy to accomplish via `execute` Ex command...


```vim
execute 'normal I#' . repeat('=', 38) . '#'
```


This trick may also be used within Vim scripts, such as inserting HTML open/close tags and repositioning the cursor...


```vim
function! insert_html_tag(name) abort
  execute 'normal i<' . name . '></' . name '>'
  let l:cursor_position = getpos('.')
  let l:cursor_position[1] -= length(name) + 3
  call setpos('.', l:cursor_position)
endfunction
```


**Example usage**


```vim
call insert_html_tag('p')
```


**Example output**


```html
<p></p>
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

