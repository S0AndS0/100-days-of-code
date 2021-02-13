---
layout: post
title: Vim Verbatim
date: 2021-02-12 16:31:10 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick trick for inserting escape codes into Vim buffer
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Within Insert mode use <kbd>Ctrl</kbd> <kbd>v</kbd> to output the next sequence _verbatim_, this can be super helpful for generating escape sequences, eg...


```vim
i
<C-v>
<C-[>
```


... results in inserting _`^[`_ (AKA <kbd>Esc</kbd> key-code) as a single character.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

