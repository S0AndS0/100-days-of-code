---
layout: post
title: Bash enable Vi mode
date: 2020-07-22 10:48:38 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to enable Vi shortcuts within Bash shell
time_to_live: 1800
---



How to enable Vi shortcuts within Bash shell...


```bash
tee -a ~/.bash_aliases 1>/dev/null <<'EOF'
set -o vi
EOF
```


How to list bindings in Insert and Normal modes...


```bash
bind -P | grep -E '^vi'
bind -P | grep -E '^vi' ## <Esc><cr>
```


Check [Vim Fandom Wiki -- Use vi shortcuts in terminal](https://vim.fandom.com/wiki/Use_vi_shortcuts_in_terminal) for tips on how to customize bindings.


___


## Attribution
[heading__attribution]: #attribution


- [YouTube -- TFW You Learn There's a Vim Mode in Bash](https://www.youtube.com/watch?v=GqoJQft5R2E)
