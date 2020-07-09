---
layout: post
title: Vim script file type detection
date: 2020-07-09 12:33:11 -0700
#date_updated:  # Optional and formatted like Thu Jul  9 12:33:11 PDT 2020 above
description: Example of utilizing `&filetype` to detect specific file type
time_to_live: 1800
---



Example of utilizing `&filetype` to detect specific file type...


```vim
nnoremap <leader>dmd :call DetectMD()<cr>

function! DetectMD()
  if &filetype == 'markdown'
    echo 'Is a MarkDown file'
  else
    echo 'Is **not** a MarkDown file'
  endif
endfunction
```


Example usage...


```bash
vim /tmp/test.md
#$ \mdm
#> Is a MarkDown file
#$ :q

vim /tmp/test.sh
#$ \mdm
#> Is **not** a MarkDown file
#$ :q
```
