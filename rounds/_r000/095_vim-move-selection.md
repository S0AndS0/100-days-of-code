---
layout: post
title: Vim move selection
date: 2020-07-31 14:57:44 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Vim configurations to move visual selection up or down
time_to_live: 1800
---


Vim configurations to move visual selection up or down


**`~/.vimrc`**


```vim
vnoremap J :m '>+1<CR>gv=gv
vnoremap K :m '<-2<CR>gv=gv
```


<kbd>Shift</kbd><kbd>V</kbd> key combo will select a line


> <kbd>j</kbd> and <kbd>k</kbd> keys will select more (or less) lines


<kbd>Shift</kbd>^<kbd>K</kbd> key combo will move selected text up


<kbd>Shift</kbd>^<kbd>J</kbd> key combo will move selected text down


___


## Attribution
[heading__attribution]: #attribution "Resources that where helpful"


- [YouTube -- ThePrimeagen -- VIM Movements P2: 5 moves to make you better ked](https://www.youtube.com/watch?v=QN4fuSsWTbA)
