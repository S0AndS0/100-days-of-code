---
layout: post
title: Vim Tag Hopping
date: 2021-03-22 14:42:42 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Enabling builtin support for extending tags that Vim will hop between
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Today I will share a `~/.vimrc` customization that I've found to be useful for moving around a document quickly.


Normally the `%` key within Normal mode will _bounce_ the cursor location between symbols such as parenthesise and curly-braces, eg...


```javascript
function fnName(parameter) {
  /* ... */
}
```


But there is a builtin plugin/package that expands on what the `%` key will bounce between, enable via the following two configurations...


**`~/.vimrc` (snip)**


```vim
filetype plugin on
packadd! matchit
```


> The `filetype plugin on` line enables Vim package support
>
> The `packadd! matchit` line activates the _`matchit`_ package


After enabling the `matchit` packages keywords may be _bounced_ between, eg...


```bash
if true; then
  printf 'Totally\n'
else
  printf 'Nope\n'
fi
```


... the `if`, `else`, and `fi` keywords may be jumped to via the `%` key


Check the official documentation for how to further extend what `%` will match on...


```bash
vim -c ':help matchit'
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

