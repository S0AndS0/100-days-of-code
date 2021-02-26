---
layout: post
title: Vim Precise Motions
date: 2021-02-26 13:13:04 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Vim tricks for moving the cursor position with precision
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Some of the first motions learned when adopting Vim as a daily text editor are <kbd>h</kbd>, <kbd>j</kbd>, <kbd>k</kbd>, and <kbd>l</kbd> for moving the cursor left, down, up, and right respectively. These motions also accept a number prefix, eg...


- <kbd>2</kbd><kbd>h</kbd> moves the cursor two columns left

- <kbd>3</kbd><kbd>l</kbd> moves the cursor three columns right

- <kbd>9</kbd><kbd>j</kbd> moves the cursor nine rows down

- <kbd>5</kbd><kbd>k</kbd> moves the cursor five rows up


But these motions are all relative to the initial cursor position, to instead move by absolute amounts one must learn about <kbd>G</kbd> and <kbd>|</kbd> motions;


**Row Motions**


- <kbd>G</kbd> moves the cursor to the last line of current buffer/file

- <kbd>5</kbd><kbd>G</kbd> moves the cursor to the fifth line of current buffer/file

- <kbd>G</kbd><kbd>G</kbd> moves the cursor to the first line of current buffer/file


**Column Motions**


- <kbd>|</kbd> or <kbd>0</kbd> moves the cursor to the first column of current line

- <kbd>7</kbd><kbd>|</kbd> moves the cursor to the seventh column of current line

- <kbd>^</kbd> moves the cursor to the first non-blank character of current line

- <kbd>$</kbd> moves the cursor to the last column of current line

- <kbd>$</kbd><kbd>b</kbd><kbd>e</kbd> moves the cursor to the last non-blank column of current line


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

