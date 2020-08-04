---
layout: post
title: Vim jump splits
date: 2020-08-04 12:48:13 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Vim configurations to jump between splits swiftly
time_to_live: 1800
---



Vim configurations to jump between splits swiftly...


**`~/.vimrc` (snip)**


```vim
""
" Bind Ctrl^<movement> keys to move splits
" Left
nnoremap <c-h> :wincmd h<CR>
nnoremap <c-Left> :wincmd h<CR>
" Down
nnoremap <c-j> :wincmd j<CR>
nnoremap <c-Down> :wincmd j<CR>
" Up
nnoremap <c-k> :wincmd k<CR>
nnoremap <c-Up> :wincmd k<CR>
" Right
nnoremap <c-l> :wincmd l<CR>
nnoremap <c-Right> :wincmd l<CR>
```
