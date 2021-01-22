---
layout: post
title: Sed Multiple Expressions
date: 2021-01-21 21:34:21 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick tips on how to use multiple expressions with Sed command-line tool
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Today I had to do some bulk renaming of class names for a JavaScript project that will be published later this week, thankfully there are command-line programs such as Sed that make this process relativly painless.


As an example, here's how to change `spam` to `Spam`, and `ham` to `Ham` with one command...


**`example-file.ext`**


```
spam flavored ham
```


```bash
sed -i '{
  s#spam#Spam#g;
  s#ham#Ham#g;
}' example-file.txt
```


**`example-file.ext`**


```
Spam flavored Ham
```


... Spiffier still is that Sed, like many other command-line applications for GNU Linux, may take a space sperated list of files, eg...


```bash
sed -i '{
  s#spam#Spam#g;
  s#ham#Ham#g;
}' file-one.txt file-two.ext # ...
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

