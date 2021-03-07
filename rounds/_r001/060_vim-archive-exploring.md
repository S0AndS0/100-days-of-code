---
layout: post
title: Vim Archive Exploring
date: 2021-03-05 14:34:53 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Overview of archive related Vim builtin features I was happy to find
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1367969086844661767
  title: Link to Tweet for this post
---



When writing the [Vim Configure Thesaurus][link__post__vim_configure_thesaurus] post I accidentally ran _`vim /tmp/thesaurus_pkg.zip`_ which started the default file explorer for Vim, and had no problems exploring the file archive as though it where a normal folder!


Suffice to say, I was so pleased that I had to share.


What's more is that there are other file extensions this feature functions with, so far I've tested the following to work with the default Vim file explorer;


- `jar` Java archive

- `gz` GNU Zip archive

- `tar` Tape archive

- `zip` File archive


More information may be available via Vim `:help` documentation


- `vim -c ':help netrw'`

- `vim -c ':help :Explore'`


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

