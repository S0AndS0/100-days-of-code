---
layout: post
title: Vim script arbitrary arguments
date: 2020-07-18 12:18:58 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example Vim script function that accepts arbitrary number of arguments
time_to_live: 1800
category: vim
---



Example Vim script function that accepts arbitrary number of arguments...


```vim
function! Test_Args(...)
  let stringed_args = join(a:000)
  echo 'l:stringed_args ->' l:stringed_args
endfunction

call Test_Args('spam', 'flavored', 'ham')
"> l:stringed_args -> spam flavored ham
```


... the _magic sauce_ is declaring a function that accepts ellipsis (`...`) as an argument. And using `a:000` concatenates all elements of the argument array.
