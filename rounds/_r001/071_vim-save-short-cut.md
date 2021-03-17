---
layout: post
title: Vim Save Short-cut
date: 2021-03-16 16:27:29 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Configurations I use for quickly saving a file buffer
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1371968286334803969
  title: Link to Tweet for this post
---



Saving while writing is important to avoid loss of data from unexpected events.


In many graphical text editors the <kbd>Ctrl</kbd> <kbd>s</kbd> keyboard shortcut is used for quickly saving a file. However, in Vim this can cause issues because that keyboard shortcut in terminals will _pause_ execution. Instead in Vim it is common to form muscle memory of, <kbd>Esc</kbd><kbd>Esc</kbd> then `:w`, to write buffer a file.


Personally I find the sequence of pressing five to six keys for saving a file less than desirable. Furthermore on devices with solid-state storage such as; memory card, USB flash, etc. the `:write` command may cause unnecessary wear-and-tear. Because the `:write` command does **not** check if the buffer and file are at all different before saving.


Fortunately there be a _smarter_ way to save files via the `:update` command...


```bash
vim -c 'help :update'
```


> `Like ":write", but only write when the buffer has been modified.`


... And armed with knowledge on remapping keys it is possible to define custom keyboard shortcuts for saving a buffer only when it has unsaved changes, eg...


**`~/.vimrc` (snip)**


```vim
" Quick-save
nnoremap <C-Z> :update<CR>
vnoremap <C-Z> <C-C>:update<CR>
inoremap <C-Z> <C-O>:update<CR>
```


With the above configurations pressing <kbd>Ctrl</kbd> <kbd>z</kbd> in Normal, Visual, or Insert modes will run the `:update` command! The only caveat is the Visual mode mapping currently will also exit that mode too, but after many months I've yet to consider this irksome enough to resolve.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

