---
layout: post
title: Git Diff Tips
date: 2021-03-04 15:20:33 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick `git diff` command-line tip
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



One of the _`git diff`_ options I've been utilizing recently is an option that diffs between last commit and changes staged for commit...


```bash
git diff --staged
# ... Or...
git diff --cached
```


... This allows me to quickly pickup where I left off from a previous day, well so long as I remembered to preform a _`git add`_ without immediately committing changes.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

