---
layout: post
title: Vim Ex to STDOUT
date: 2021-03-30 16:23:04 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to redirect Ex mode command output to standard out
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1377040164283940869
  title: Link to Tweet for this post

attribution:
  links:
    - text: VI StackExchange -- vim ex mode write to stdout
      href: https://vi.stackexchange.com/questions/23198/
      title: vim ex mode write to stdout
      class: fa fa-stack-overflow

    - text: StackOverflow -- Omitting the first line from any Linux command output
      href: https://stackoverflow.com/questions/7318497/
      title: Omitting the first line from any Linux command output
      class: fa fa-stack-overflow
---



One of the projects that I'm working on involves obtaining the directory path to system level Vim configurations. Within a Vim session the `$VIM` variable may be inspected, eg...


```vim
echo $VIM
"> /usr/local/share/vim
```


... however, for my use case the output needs to be written to STDOUT (Standard Out) such that a shell script may use the path.


Fortunately there are command-options for running a sequence of Vim Ex mode commands, as well as builtin methods for redirecting Ex mode command output to a file.


```bash
_vim_sys_dir="$(vim -e -s -c 'redi! > /dev/stdout | echo $VIM | redi END | qa' | tail -n +2)"

printf '%s\n' "${_vim_sys_dir}"
#> /usr/local/share/vim
```


**Vim Options**


- `-e` Start Vim in Ex mode, just like the executable was called "ex".

- `-s` Silent mode.  Only when started as "Ex" or when the "-e" option was given before the "-s" option.

- `-c` **{command}** will be executed after the first file has been read.

- `redi! > __path__` ... `redi END` redirects output to file `__path__`, note `>>` instead of `>` will append instead of overwrite

- `|` vertical-bars separate commands, similar to semicolons (`;`) in other languages


**Tail Options**


- `-n +2` Start passing through on second line of output


---


For larger operations it may be useful to define a Vim function similar to the following for redirecting multiple commands to Standard Out...


```vim
function! Ex2STDOUT(...) abort
  let l:results = split(execute(a:000), '\n')

  for l:result in l:results
    redi! > /dev/stdout
      echo l:result
    redi END
  endfor
endfunction
```


... use within Vim via `:call` Ex mode keyword...


```vim
call Ex2STDOUT('echo "hello"', 'echo "world"')
```


... or via shell by sourcing the file and calling directly, eg...


```bash
vim -e -s -c "source .vimrc | call Ex2STDOUT('echo \"hello\"', 'echo \"world\"') | qa" | tail -n +2
```


> Side note, I've yet to figure out how to suppress the first blank line when redirecting output this way


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

