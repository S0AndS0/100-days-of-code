---
layout: post
title: Vim Replace Visual Selection
date: 2021-01-08 15:32:59 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick Vim tip for find/replace text within Visual mode selection
time_to_live: 1800

attribution:
  links:
    - text: 'Vi -- StackExchange -- How to replace only within visual selection?'
      href: https://vi.stackexchange.com/questions/1922/
      title: 'How to replace only within visual selection?'
      class: 'fa fa-stack-exchange'
---



Visual select mode has three sub-modes that can be initialized from Normal mode;

0. <kbd>v</kbd> key will start Visual select mode that follows the cursor start/end postion

1. <kbd><kbd>Shift</kbd><kbd>V</kbd></kbd> key combo will select by line

2. <kbd><kbd>Ctrl</kbd><kbd>V</kbd></kbd> key combo will select a _block_ of text


Regardless of mode, once a selection has been made it is possible to restrict find/replace Ex commands to only selected text, for example to replace all `-` with a space would be similar to...


```vim
:'<,'>s/\%V-/ /g
```


**Explanation**


- `'<,'>` portion is automatically prepended to Ex mode commands started from Visual mode

- `s` bit is an abbreviation for _search_

- `\%V` sequence is the _magic sauce_ that restricts search expression to only what was selected. Check `:help \%V` documentation for details.

- `-` character may be any search expression, eg. `^[0-1]`

- trailing `g` causes find/replace command to be executed _globally_ for the selected text


---

