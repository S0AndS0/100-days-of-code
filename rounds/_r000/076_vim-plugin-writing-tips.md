---
layout: post
title: Vim plugin writing tips
date: 2020-07-12 10:57:00 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Examples and tips on writing and installing Vim plugin
time_to_live: 1800
category: vim
---



Examples and tips on writing and installing Vim plugin


## Write Plugin Script
[heading__write_plugin_script]: #write-plugin-script


**`hello-vim/plugin/hello-vim-greeter.vim`**


```vim
nnoremap <leader>vg :call Hello_Vim_Greeter()<cr>
command! -nargs=* VG call Hello_Vim_Greeter(<f-args>)


""
" Greets world or provided arguments
function! Hello_Vim_Plugin(...)
  let greeting_string = join(a:000)
  if len(l:greeting_string)
    echo 'Hello ' . l:greeting_string . '!'
  else
    echo 'Hello world!'
  endif
endfunction
```


___


## Write Plugin Help
[heading__write_plugin_help]: #write_plugin_help


**`hello-vim/doc/hello-vim-greeter.txt`**


```txt
*hello-vim-greeter.txt*     For Vim version 8.0.     Last change: 2020 Jul 12


                       Hello Vim Greeter    by S0AndS0


MarkDown Heading Transform                                *hello-vim-greeter*

1. Leader commands                                  |hello-vim-greeter-leader|
2. Commands                                        |hello-vim-greeter-command|

==============================================================================
1. Leader commands                                  *hello-vim-greeter-leader*

                   *vg*
<Leader>vg         Greet the world example: >
                       \vg

<                  Echos "Hello World!"

==============================================================================
2. Commands                                        *hello-vim-greeter-command*

                   *VG*
:VG                Greet names specified by arguments list example:  >
                       :VG Bill and Ted

<                  Echos "Hello Bill and Ted!"


 vim:tw=78:ts=8:ft=help:norl:
```


> Note, columns in help documentation should be **tab** separated!


When writing documentation files with Vim use the following commands to toggle syntax highlighting...


- `set filetype=text` turns **off** syntax highlighting

- `set filetype=help` turns **on** syntax highlighting


___


## Install Without Plugin Manager
[heading__install_without_plugin_manager]: #install-without-plugin-manager


```bash
cd ~/git/hub/vim-utilities/hello-vim

mkdir -vp ~/.vim/plugin/hello-vim
mkdir -vp ~/.vim/doc

ln -s "${PWD}/plugin" "${HOME}/.vim/plugin/hello-vim/"
ln -s "${PWD}/doc/*" "${HOME}/.vim/doc/"

vim -c ':helptags ~/.vim/doc' -c ':q'
```


## Attribution
[heading__attribution]: #attribution


- Vim documentation

  - `:help helphelp.txt`
  - `:help help-writing`
  - `:help add-local-help`
  - `:help write-local-help`
