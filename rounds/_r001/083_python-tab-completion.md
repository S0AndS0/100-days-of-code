---
layout: post
title: Python Tab Completion
date: 2021-03-28 16:12:36 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Configuration to enable tab-completion within Python shell
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1376312172813377536
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How do I add tab completion to the Python shell?
      href: https://stackoverflow.com/a/246779/2632107
      title: How do I add tab completion to the Python shell?
      class: fa fa-stack-overflow
---



One of the modifications I make to any Linux system I plan to work with for Python programming is enabling tab-completion via the following two file modifications...


**`~/.pythonrc`**


```python
try:
    import readline
except ImportError:
    print('Module readline not available.')
else:
    import rlcompleter
    readline.parse_and_bind('tab: complete')
```


Above file will attempt to find, and utilize, the `readline` package or fail silently.


Bellow should be appended to the `~/.bashrc` file to ensure above file is sourced when an interactive Python shell is initialized...


**`~/.bashrc`**


```bash
export PYTHONSTARTUP=~/.pythonrc
```


... with those two edits most systems will be fully ready to expand command/method calls, eg...


```python
s = ''
s.__
```


... pressing <kbd>Tab</kbd> twice after the `s.__` should produce output similar to...


```
s.__add__(           s.__getattribute__(  s.__len__(           s.__repr__(
s.__class__(         s.__getitem__(       s.__lt__(            s.__rmod__(
s.__contains__(      s.__getnewargs__(    s.__mod__(           s.__rmul__(
s.__delattr__(       s.__getslice__(      s.__mul__(           s.__setattr__(
s.__doc__            s.__gt__(            s.__ne__(            s.__sizeof__(
s.__eq__(            s.__hash__(          s.__new__(           s.__str__(
s.__format__(        s.__init__(          s.__reduce__(        s.__subclasshook__(
s.__ge__(            s.__le__(            s.__reduce_ex__(     
```


______



## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

