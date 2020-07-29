---
layout: post
title: Vim auto-close braces
date: 2020-07-29 12:33:38 -0700
#date_updated:  # Optional and formatted like 'date' above
description: VimRC example for automatically closing braces/brackets
time_to_live: 1800
---



VimRC example for automatically closing braces/brackets...


**`~/.vimrc`**


```vim
:inoremap ( ()<left>
:inoremap [ []<left>
:inoremap { {}<left>
```


___


## Attribution
[heading__attribution]: #attribution "Resources that were helpful in building above examples"


- [Reddit -- How do I make Vim automatically complete](https://www.reddit.com/r/vim/comments/bsh7da/how_do_i_make_vim_automatically_complete/)

