---
layout: post
title: Vim MarkDown Syntax Highlighting
date: 2021-04-05 16:43:21 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Quick how-to for enabling syntax highlighting within MarkDown files
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://example.com
  title: Link to Tweet for this post
---


One of the things I liked about Atom, and other IDEs, was syntax highlighting within MarkDown code blocks, eg...


    ```bash
    #!/usr/bin/evn bash
    echo 'Hello world'
    ```


... But I found recently that Vim has this capability too!


**`~/.vimrc` (snip)**


```vim
let g:markdown_minlines = 100

let g:markdown_fenced_languages = [
     \   'awk'
     \   'bash=sh'
     \   'css'
     \ ]
```


The `g:markdown_minlines` variable defines how many lines, above and bellow, that Vim should search for triple backtics. Note, setting this to large may degrade performance when editing/viewing MarkDown files within Vim.


The `g:markdown_fenced_languages` variable defines a list of languages that Vim will attempt to preform syntax highlighting within code blocks.


Supported languages may be found within the `syntax/` subdirectory of the Vim install path, use the following command to find the Vim runtime path...


```vim
echo $VIMRUNTIME
```


**Warning**, adding `markdown` to the list of fenced languages will cause errors, and beware some languages will source other syntax files! Or in other words, be selective of what languages to enable syntax highlighting for within MarkDown files.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

