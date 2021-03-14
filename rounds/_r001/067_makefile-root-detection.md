---
layout: post
title: Makefile Root Detection
date: 2021-03-12 12:31:51 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to set Makefile variables based on permissions
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1370525989743247366
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How to check if running as root in a bash script
      href: https://stackoverflow.com/questions/18215973/
      title: How to check if running as root in a bash script
      class: fa fa-stack-overflow
---



For my most recently published project I wanted to configure installation variables based on if `make` commands where run with, or without, root level permissions.


Here's a quick, self-contained example...


**`Makefile`**


```make
#!/usr/bin/make -f


ifeq '$(shell id -u)' '0'
	IS_ROOT := true
else
	IS_ROOT := false
endif


.PHONY: debug
.SILENT: debug


debug: SHELL := /bin/bash
debug: ## Prints make variables
	echo "$(IS_ROOT)"
```


... Above may be run via `make debug` and `sudo make debug`


> Note, `0` from _`id -u`_ is generally the level of root and anything else is a _normal_ account


And here's a snip from a _live_ project Make file...


```make
ifeq '$(shell id -u)' '0'
	INSTALL_DIRECTORY := /usr/local/sbin
	COMPLETION_DIR := $(shell pkg-config --variable=completionsdir bash-completion)
else
	COMPLETION_DIR := $(shell echo "$${BASH_COMPLETION_USER_DIR:-$${HOME}/.local/share/bash-completion}")
	INSTALL_DIRECTORY := $(HOME)/bin
endif
```


> Note, doubled dollar signs (`$$`) are the way to denote a literal dollar sign, without escaping Make would attempt to parse as an internal variable/command.


This trick _should_ function for most, if not all, 'nix-like operating systems. And suggestions for how to check admin permissions for MicroSoft devices would be swell.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

