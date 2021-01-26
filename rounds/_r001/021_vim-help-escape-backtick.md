---
layout: post
title: Vim Help Escape Backtick
date: 2021-01-25 18:51:55 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to display literal backtick input within Vim help documentation
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Today while documenting a Vim plugin that I'll be publishing later this week issues where had trying to document backtick input. This is because backticks surround certain keywords within `help` files, similar to MarkDown syntax, however, unlike other syntaxes prefixing with a backslash (`\`) didn't have the desired effect.


Where things to operate as expected one could write something like...


```vimhelp
Something about `\`` usage within some mode
```


But the closest I could get was using angle-brackets similar to...


```vimhelp
>
  `
< Some text about backticks
```


... For now is good enough for my use cases, however, readers should be aware of some caveats;


- Greater-than (`>`) may have characters prior, but cannot have characters following on the same line

- Less-than (`<`) cannot have characters prior, but may have characters following on the same line

- Characters between greater-than and less-than blocks must be indented by at least two spaces (`  `) or one tab (`\t`)


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

