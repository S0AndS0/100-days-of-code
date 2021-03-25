---
layout: post
title: Vim NetRW Customization
date: 2021-03-25 11:57:54 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Few `.vimrc` tweaks I have found useful
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post

attribution:
  links:
    - text: "Shape Shed -- Vim: you don't need NERDtree or (maybe) netrw"
      href: https://shapeshed.com/vim-netrw/
      title: "Vim: you don't need NERDtree or (maybe) netrw"

    - text: GitHub -- `changemewtf/no_plugins` -- Vim 90% IDE Without Plugins
      href: https://github.com/mcantor/no_plugins
      title: Vim 90% IDE Without Plugins
      class: fa fa-github
---


The following configurations are, as of 2021-03-25, what I'm using to customize NetRW...


**`~/.vimrc` (snip)**


```vim
""
" NetRW customization
let g:netrw_banner = 0        " suppress the banner
let g:netrw_browse_split = 4  " open previous window
let g:netrw_altv = 1          " open splits to the right
let g:netrw_liststyle = 3     " tree style listing


let g:netrw_hide = 1          " show not-hidden files
let g:netrw_list_hide = '.*\.swp$'


""
" Open left vertical split for NetRW
function! s:Project_Drawer__NetRW() abort
  if expand('%') == '.git/COMMIT_EDITMSG'
    return
  endif

  if $PWD == $HOME
    return
  endif

  :Lexplore $PWD
endfunction


let g:netrw_winsize = 15
augroup ProjectDrawer
  autocmd!
  autocmd VimEnter * :call s:Project_Drawer__NetRW()
augroup END
```


... Effectively these configurations ensure that new Vim sessions also start with a NetRW split, except when writing Git commits or when opening files while current working directory is _`$HOME`_.


I'm still learning the capabilities of NetRW so suggestions are certainly welcomed!


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

