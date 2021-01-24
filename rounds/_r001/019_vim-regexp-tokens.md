---
layout: post
title: Vim RegExp Tokens
date: 2021-01-23 20:10:18 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to use Regular Expressions with Vim find/replace commands
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
    - text: 'StackOverflow -- Vim: Find and replace, reuse token'
      href: https://stackoverflow.com/questions/12286968/
      title: 'Vim: Find and replace, reuse token'
      class: fa fa-stack-overflow
---



Today while writing documentation for a project I wanted to cross-link bits via heading IDs, for example I wanted all instances of `**{Iterator_Cascade_Callbacks}**` to link to the relevant section within the same document...


```markdown
#### Method `Callback_Object.call`
[heading__method_callback_objectcall]:
  #method-callback_objectcall
  "Calls `this.wrapper` function with reference to this `Callback_Object` and `Iterator_Cascade_Callbacks`"


Calls `this.wrapper` function with reference to this `Callback_Object` and `Iterator_Cascade_Callbacks`


**Parameters**


- **{Iterator_Cascade_Callbacks}** `iterator_cascade_callbacks` - Reference to `Iterator_Cascade_Callbacks` instance


=======================
... _other content_ ...
=======================


### Class `Iterator_Cascade_Callbacks`
[heading__class_iterator_cascade_callbacks]:
  #class-iterator_cascade_callbacks
  "Iterator that chains callback function execution"


Iterator that chains callback function execution
```


... I could have cross-linked things manually similar to...


```markdown
- [**{Iterator_Cascade_Callbacks}**][heading__class_iterator_cascade_callbacks] `iterator_cascade_callbacks` - Reference to `Iterator_Cascade_Callbacks` instance
```


... However, Vim has some fantastic options via Ex mode, so instead I wrote one command to find and replace all instances of _`**{Iterator_Cascade_Callbacks}**`_ with _`[**{Iterator_Cascade_Callbacks}**][heading__class_iterator_cascade_callbacks]`_


```vim
:%s/\(\*\*{Iterator_Cascade_Callbacks}\*\*\)/[\1][heading__class_iterator_cascade_callbacks]/g
```


Breakdown of above command;


- `%s/` searches, and the `%` potion tells Vim to search the whole document; if `%` where omitted then search would be restricted to current line

- `\(\)` parenthesis tag/group a portion of RegExp, these are numbered in order such that `\1` through `\_n_` can be used within the replace portion of the command

- `*` (asterisks) must be escaped to prevent RegExp interoperation

- `\1` references the first match group


Utilizing this trick I was able to add cross-linking where applicable throughout the entire document swiftly!


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

