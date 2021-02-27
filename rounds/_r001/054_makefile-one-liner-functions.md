---
layout: post
title: Makefile One-liner Functions
date: 2021-02-27 14:00:02 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick how-to on writing and using Makefile script functions
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Make scripts have a concise way of defining and calling simple functions. Definition is similar to any other variable _`name = value`_, except that numbered parameters _`$(1)`_ may be used. And using said definitions is facilitated via `call` command, eg...


**`Makefile`**


```make
nix_path_append = $(strip $(1))/$(strip $(2))

win_path_append = $(strip $(1))\\$(strip $(2))


.PHONY: debug-nix debug-win
.SILENT: debug-nix debug-win


debug-nix:
	@echo $(call nix_path_append, foo, bar)

debug-win:
	@echo $(call win_path_append, canned, spam)
```


**Example usage**


```bash
make debug-nix
#> foo/bar

make debug-win
#> canned\spam
```


... At the time of writing this post however, I've yet to sort out how to pass an arbitrary list of parameters.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

