---
layout: post
title: Vim Current Character
date: 2021-01-06 13:26:33 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick Vim script tip on saving a character under the cursor to a variable
time_to_live: 1800

tweet:
  url: https://twitter.com/S0_And_S0/status/1346976643898880000
---



I invested much of today towards writing documentation files for a Vim plugin that'll be published in a couple of days. To tide readers over until then, here's a quick Vim script for obtaining a character under the cursor...


```vim
echo getline('.')[col('.') - 1]
```


And a short function that may be used within scripts...


```vim
function Current_Character() abort
  let l:current_character = getline('.')[col('.') - 1]
  return l:current_character
endfunction
```


... along with an example of echoing the output...


```vim
echo Current_Character()
```


So far I've found this trick to be useful within plugins that register Insert mode mappings. In particular the plugin that'll soon be published will take into account what key was pressed, along with what character the cursor is on, and use both bits of information to determine if a character is inserted or the cursor is moved.

