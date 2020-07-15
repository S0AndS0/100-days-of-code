---
layout: post
title: Vim spelling shortcuts
date: 2020-07-06 10:37:41 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Vim script plugin example
time_to_live: 1800
---



Vim scripts can be saved as plugins via the following path syntax...


```
~/.vim/plugin/<name>/plugin/<name>.vim
```


... for example auto-loading a spelling shortcuts plugin could have a path similar to...


```
~/.vim/plugin/spelling-shortcuts/plugin/spelling-shortcuts.vim
```


Example `spelling-shortcuts` Vim script plugin...


**`~/.vim/plugin/spelling-shortcuts/plugin/spelling-shortcuts.vim`**


```vim
nnoremap <leader>sp :call FixLastSpelling()<cr>
nnoremap <leader>sn :call FixNextSpelling()<cr>

function! FixLastSpelling()
  normal! mm[s1z=`m
endfunction

function! FixNextSpelling()
  normal! mm]s1z=`m
endfunction
```


## Attribution
[heading__attribution]: #Attribution


- [YouTube -- Your First Vim Plugin](https://www.youtube.com/watch?v=lwD8G1P52Sk)
