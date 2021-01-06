---
layout: post
title: Vim Plugin Setup
date: 2021-01-05 18:37:46 -0800
#date_updated:  # Optional and formatted like 'date' above
description: An overview of how I setup a new Vim plugin project
time_to_live: 1800
---



Today was dedicated to preparing a new Vim plugin for publishing later this week, so it seemed like a good idea to cover some of the setup steps I use for writing plugins.


---


- [Organization Setup][heading__organization_setup]

- [Git Initialization][heading__git_initialization]

- [Plugin Directories and Files][heading__plugin_directories_and_files]

- [Plugin Documentation Template][heading__plugin_documentation_template]

- [Plugin Script Template][heading__plugin_script_template]

- [Manual Install][heading__manual_install]

- [Git Directories and Files][heading__git_directories_and_files]

- [Publish Publicly][heading__publicly_publish]

- [Questions, Comments, or Suggestions][heading__questions_comments_or_suggestions]


---


## Organization Setup
[heading__organization_setup]: #organization-setup


GitHub Organizations that I administrate are organized under their own sub-directories, eg...


```bash
mkdir -p ~/git/hub/vim-utilities

cd ~/git/hub/vim-utilities
```


---


## Git Initialization
[heading__git_initialization]: #git-initialization


After changing current working directory to the `vim-utilities` sub-directory creating a new Git repository with a short, and descriptive, name is a good idea. And again the current working directory is changed, this time to the root of the new Git repository...


```bash
git init balanced-braces

cd ~/git/hub/vim-utilities/balanced-braces
```


---


## Plugin Directories and Files
[heading__plugin_directories_and_files]: #plugin-directories-and-files


Next task is creating directories and files specific to authoring Vim plugins...


```bash
mkdir doc
touch doc/balanced-braces.txt

mkdir plugin
touch plugin/balanced-braces.vim
```


---


## Plugin Documentation Template
[heading__plugin_documentation_template]: #plugin-documentation-template


A template to populate the `doc/balanced-braces.txt` file helps with consistency, and mitigates forgetting commonly useful sections...


```vimhelp
*balanced-braces.txt*      For Vim version 8.0.       Last change: 2021 Jan 05


                      Balanced Quotes    by S0AndS0


Balanced Quotes                                              *balanced-braces*

1. Insert Map Defaults                            |balanced-braces-insert-map|
2. Functions                                       |balanced-braces-functions|
3. Configuration                               |balanced-braces-configuration|
4. Notes                                               |balanced-braces-notes|

==============================================================================
1. Insert Map Defaults                            *balanced-braces-insert-map*

==============================================================================
2. Functions                                       *balanced-braces-functions*

==============================================================================
3. Configuration                               *balanced-braces-configuration*

==============================================================================
4. Notes                                               *balanced-braces-notes*

 vim:tw=78:ts=8:ft=help:norl:
```


> Note, check the following built-in Vim documentation topics for details
>
> - `:help helphelp.txt`
> - `:help write-local-help`
> - `:help add-local-help`




---


## Plugin Script Template
[heading__plugin_script_template]: #plugin-script-template


For the `plugin/balanced-braces.vim` script a starter template similar to the following may be helpful...


```vim
#!/usr/bin/env vim
" balanced-braces.vim - Attempts to balance symbols and quotes
" Version: 0.0.1
" Maintainer: S0AndS0 <https://github.com/S0AndS0>
" License: AGPL-3.0


""
" Fast finish if already loaded or Vim version is bellow target
if exists('g:balanced_braces__loaded') || v:version < 700
  finish
endif
let g:balanced_braces__loaded = 1


""
" Merged dictionary without mutation
" Parameter: {dict} defaults
" Parameter: {dict} override
" Return: {dict}
" See: {docs} :help type()
" See: {link} https://vi.stackexchange.com/questions/20842/how-can-i-merge-two-dictionaries-in-vim
function! s:Dict_Merge(defaults, override, ...) abort
  let l:new = copy(a:defaults)

  for [l:key, l:value] in items(a:override)
    if type(l:value) == type({}) && type(get(l:new, l:key)) == type({})
      let l:new[l:key] = s:Dict_Merge(l:new[l:key], l:value)
    else
      let l:new[l:key] = l:value
    endif
  endfor

  return l:new
endfunction


""
" ... Plugin specific functions should be added here...


""
" Configurations that may be overwritten
let s:defaults = {}


""
" Merge configuration modifications with defaults
" See: {docs} :help fnamemodify()
" See: {docs} :help readfile()
" See: {docs} :help json_decode()
if exists('g:balanced_braces')
  if type(g:balanced_braces) == type('') && fnamemodify(g:balanced_braces, ':e') == 'json'
    let g:balanced_braces = json_decode(readfile(g:balanced_braces))
  endif

  if type(g:balanced_braces) == type({})
    let g:balanced_braces = s:Dict_Merge(s:defaults, g:balanced_braces)
  else
    let g:balanced_braces = s:defaults
  endif
else
  let g:balanced_braces = s:defaults
endif


""
" ... Registration of mode mapping should be added here...
```


For manual installation


```bash
ln -s ~/git/hub/vim-utilities/balanced-braces ~/.vim/plugin/
```


---


## Manual Install
[heading__manual_install]: #manual-install


By default Vim will search the `~/.vim/doc` directory for user installed documentation, inserting symbolic links is an easy way of reducing overhead, eg...


```bash
ln -s ~/git/hub/vim-utilities/balanced-braces/doc/balanced-braces.txt ~/.vim/doc/
```


... Beware that to have `:help` commands jump to the correct file and/or section, the `helptags` file should be updated...


```bash
vim -c ":helptags ${HOME}/.vim/doc" -c ':q'
```


Vim plugins that do **not** require `&runtimepath` modification may use a symbolic link to `~/.vim/plugin/` directory, eg...


```bash
ln -s ~/git/hub/vim-utilities/balanced-braces ~/.vim/plugin/
```


> Note; generally plugin managers will handle linking, and updating the Vim `helptags` file. Often instead of making symbolic links, plugin managers instead append to the `&runtimepath` variable.


---


## Git Directories and Files
[heading__git_directories_and_files]: #git-directories-and-files


After writing and testing plugin script(s), and filling-out documentation file(s), it's time to focus on populating Git specific directories and files...


```bash
tee -a .gitignore 1>/dev/null <<'EOF'
*.swp
EOF


mkdir .github
touch .github/README.md


touch LICENSE
```


> Note, for most projects I'll utilize the [`github-utilities/make-readme`][link__github_utilities__make_readme] project for starting a formatted `ReadMe` file and choosing a License.


---


## Publicly Publish
[heading__publicly_publish]: #publicly-publish


Once testing and refactoring is complete, the plugin _should_ be ready to publicly publish...


```bash
git checkout -b main


git add .github\
        .gitignore\
        LICENSE\
        doc\
        plugin


git commit -F- <<'EOF'
:tada: Initial commit...
EOF


git remote add hub "git@github.com:vim-utilities/balanced-braces.git"
git push hub main
```

---


## Questions, Comments, or Suggestions
[heading__questions_comments_or_suggestions]: #questions-comments-or-suggestions


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github_utilities__make_readme]: https://github.com/github-utilities/make-readme "Makes new ReadMe file for GitHub repository"

[link__github__s0ands0__100_days_of_code]: https://github.com/S0AndS0/100-days-of-code "Source code and posts for this site"

[link__twitter__s0_and_s0]: https://twitter.com/S0_And_S0/ "Link to @S0_And_S0 of Twitter"

