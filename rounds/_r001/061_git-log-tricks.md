---
layout: post
title: Git Log Tricks
date: 2021-03-06 16:20:30 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Some useful tips and tricks for Git logging
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1368357541697253390
  title: Link to Tweet for this post
---



Two of the most used Git logging command-line options I use are the `--oneline` parameter with `log`, and `whatchanged` option.


The `--oneline` parameter provides a condensed view of commit history...


```bash
git log --oneline
```


Each line will have a short hash, and commit title/heading, with an optional list of `remote/branch` for a given committed state.


**Example output**


```text
baf5cd9 (HEAD -> gh-pages, srv/gh-pages, hub/gh-pages) :memo: Adds post Vim Archive Exploring
3b7017e :memo: Adds link to related tweet
0fe3a99 :memo: Adds post Git Diff Tips
```


When combined with a limit, via `-<number>`, I've found this to be supper useful for checking the state of a repository, eg...


```bash
git log --oneline -3
```


---


To check commit **and** file change history I've found the `whatchanged` option to be superb, eg...


```bash
git whatchanged -3
```


**Example output**


```text
commit baf5cd95fca36c7304892388c2824d53e6edd8e6 (HEAD -> gh-pages, srv/gh-pages, hub/gh-pages)
Author: S0AndS0 <name@domain.tld>
Date:   Fri Mar 5 14:42:38 2021 -0800

    :memo: Adds post Vim Archive Exploring

:000000 100644 0000000 26bd511 A        rounds/_r001/060_vim-archive-exploring.md

commit 3b7017eba801d8975a2c9a24c88ff26b981aea16
Author: S0AndS0 <name@domain.tld>
Date:   Fri Mar 5 14:42:37 2021 -0800

    :memo: Adds link to related tweet

:100644 100644 998ead4 c18007b M        rounds/_r001/059_git-diff-tips.md

commit 0fe3a996f39e4da3aec0d90ab7387d1af4da6e8d
Author: S0AndS0 <name@domain.tld>
Date:   Thu Mar 4 15:22:25 2021 -0800

    :memo: Adds post Git Diff Tips

:000000 100644 0000000 998ead4 A        rounds/_r001/059_git-diff-tips.md
```


Pro-tip, `whatchanged` may be combined with most other `log` parameters, eg...


```bash
git whatchanged --oneline -3
```


**Example output**


```text
baf5cd9 (HEAD -> gh-pages, srv/gh-pages, hub/gh-pages) :memo: Adds post Vim Archive Exploring
:000000 100644 0000000 26bd511 A        rounds/_r001/060_vim-archive-exploring.md
3b7017e :memo: Adds link to related tweet
:100644 100644 998ead4 c18007b M        rounds/_r001/059_git-diff-tips.md
0fe3a99 :memo: Adds post Git Diff Tips
:000000 100644 0000000 998ead4 A        rounds/_r001/059_git-diff-tips.md
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

