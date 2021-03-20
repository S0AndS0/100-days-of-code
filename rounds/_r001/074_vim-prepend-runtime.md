---
layout: post
title: Vim Prepend Runtime
date: 2021-03-19 15:42:42 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Quick tip for Vim plugin authors
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1373043420730683395
  title: Link to Tweet for this post
---



In most cases the plugin setup described in [`r001/001_vim-plugin-setup`][link__100_days_of_code__r001_001__vim_plugin_setup] is adequate, however, there are instances where a Vim plugin needs included within the _`runtimepath`_ list.


Before committing a plugin to run time path modification, the Vim help documentation is worth reviewing...


```bash
vim -c ':help runtimepath'
```


So far the most concise way I've found to achieve _`runtimepath`_ prepending is via something similar to...


```vim
let s:script_parent_directory = fnamemodify(resolve(expand('<sfile>:p')), ':h:h')

execute 'set runtimepath=' . s:script_parent_directory . ',' . &runtimepath
```


______


## Explanations


**`s:script_parent_directory`**


- `fnamemodify()` function, will modify a filename (string) with defined modifiers; in the case of above the _`:h:h`_ bit removes the last two path components

- `resolve()` function, attempts to resolve shortcut/symbolic-links to the true target path

- `expand('<sfile>:p')` function, expands the _`<sfile>`_ command to the path of current script; the _`:p`_ modifier returns the parent directory


**`execute`**


- `execute` is similar to _`eval`_ in other languages in that a string is treated as a command

- The `runtimepath` variable is a comma separated list of directory paths

- `&runtimepath` expands to value within `runtimepath` prior to modification


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__100_days_of_code__r001_001__vim_plugin_setup]: {{ 'r001/001_vim-plugin-setup/' | absolute_url }}

