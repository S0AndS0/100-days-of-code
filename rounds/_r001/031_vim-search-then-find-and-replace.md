---
layout: post
title: Vim Search then Find and Replace
date: 2021-02-04 13:14:43 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Slightly advanced Vim Regexp examples for targeted mass-edits
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



> Slightly advanced Vim Regexp examples for targeted mass-edits


---


- [Syntax][heading__syntax]

- [Simple Examples][heading__simple_examples]

- [Live Example][heading__live_example]

- [Contact and/or Contribute][heading__contact_andor_contribute]


---



## Syntax
[heading__syntax]: #syntax


Search current line for `__search__`, then find pattern `__find__` and replace with `__repalce__` syntax...


```vim
:/__search__/ s/__find__/__replace__/
```


Search can be expanded to entire file by prefixing with _`g`_...


```vim
:g/__search__/ s/__find__/__replace__/
```


And the find/replace command can be expanded to operate on all matches within a line by appending _`g`_...


```vim
:g/__search__/ s/__find__/__replace__/g
```


______


## Simple Examples
[heading__simple_examples]: #simple-examples


**Example File (snip)**


```text
Lorem ipsum dolor sit amet, consectetur adipiscing elit,
sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
Ut enim ad minim veniam, quis nostrud exercitation ullamco
laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure
dolor in reprehenderit in voluptate velit esse cillum dolore eu
fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident,
sunt in culpa qui officia deserunt mollit anim id est laborum.
```


The following Ex mode command will search file for _`lab`_, then find _` al`_ and replace with _` pal`_...


```vim
:g/lab/ s/ al/ pal/g
```


To restrict `__search__` to a Visual selection prefix _`\%V`_ to the pattern...


```vim
:<'>'/\%V__search__/ s/__find__/__replace__/
```


______


## Live Example
[heading__live_example]: #live-example "Example of using Regexp tricks on a real project"


I have a JavaScript project that has extensive API documentation and I want to ensure that things are cross-linked such that every reference to a class, method, type, etc. is linked to the related section that defines it.


**Example ReadMe file (snip)**


```text
    - [Type `Callback_Wrapper`][heading__type_callback_wrapper]
...
...
- [**{Callback_Wrapper}**][heading__type_callback_wrapper] `callback_wrapper` - Function wrapper that handles input/output between `Callback_Function` and `Iterator_Cascade_Callbacks`
...
...
#### Type `Callback_Wrapper`
```


For example I want the middle line of above file snip to be...


_`- [**{Callback_Wrapper}**][heading__type_callback_wrapper] `callback_wrapper` - Function wrapper that handles input/output between [`Callback_Function`][heading__type_callback_function] and `Iterator_Cascade_Callbacks``_


... so that readers can click on _`Callback_Function`_ and be taken to the relevant section, however, I do **not** want to target the table of contents _`    - [Type `Callback_Wrapper`][heading__type_callback_wrapper]`_, or heading link _`#### Type `Callback_Wrapper``_


Where it a single line within the document then a manual edit would suffice, but there are multiple lines that should refer back to the definition section. The Ex command that I used for cross-linking references was similar to...


```vim
g/\v^((\s+)|(#+))@!.*\[@!`Callback_Function`\]@!/ s/\v(`)(Callback_Function)(`)/[&][heading__type_\L\2]/gc
```


**Search Explanation**


- `\v` causes Regexp to interpret special characters without the need of escapement, check `:help /\v`

- `^` matches beginning of line(s), ie. following expression must be at the start of a line

- `()` create match groups

- `\s` is an escape code for space-like characters, such as ` ` and/or `\t` (tab)

- `+` is one or more of previous pattern

- `|` is an _OR_ eg. _`(a|b)`_ will match _`a`_ or _`b`_

- `@!` is a Vim specific Regexp code for negating previous pattern/group

- `.*` is any characters of any amount between patterns or groups

- `\[@!` and `\]@!` further restricts matches to **not** include lines that already have square-brackets surrounding the search word

- ``Callback_Function`` are the literal characters to search for


**Find Explanation**


- `\v` again causes Regexp to interpret special characters

- ``(`)`` creates match group `\1`

- `(Callback_Function)` crates match group `\2`

- ``(`)`` creates match group `\3`


**Replace Explanation**


- `&` represents characters matched by `__find__` expression(s)

- `\L` is a Vim specific way lowercase the next listed match group

- `\2` inserts the second match group from `__find__` expression(s)


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

