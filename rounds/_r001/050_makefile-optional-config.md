---
layout: post
title: Makefile Optional Config
date: 2021-02-23 15:05:03 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Makefile script example for optional configuration
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How do I check if file exists in Makefile so I can delete it
      href: https://stackoverflow.com/questions/5553352/
      title: How do I check if file exists in Makefile so I can delete it
      class: fa fa-stack-overflow

    - text: StackOverflow -- How to have config option in Makefile
      href: https://stackoverflow.com/questions/58378555/
      title: How to have config option in Makefile
      class: fa fa-stack-overflow
---



This will be a quick guide for writing a Makefile script that may be modified with an optional configuration file


**`Makefile`**


```make
#!/usr/bin/make -f


ROOT_DIRECTORY_PATH := $(realpath $(dir $(abspath $(lastword $(MAKEFILE_LIST)))))


VARIABLE_ONE = first default
VARIABLE_TWO = second default


CONFIG := $(ROOT_DIRECTORY_PATH)/.make-config
ifneq ("$(wildcard $(CONFIG))", "")
	include $(CONFIG)
endif


.PHONY: clean config debug
.SILENT: clean config debug


clean: SHELL := /bin/bash
clean: ## Removes configuration file
	[[ -f "$(CONFIG)" ]] && {
		rm -v "$(CONFIG)"
	}

config: SHELL := /bin/bash
config: ## Writes configuration file
	tee "$(CONFIG)" 1>/dev/null <<EOF
	VARIABLE_ONE = $(VARIABLE_ONE)
	VARIABLE_TWO = $(VARIABLE_TWO)
	EOF

debug: SHELL := /bin/bash
debug: ## Prints variables and assigned variables
	echo "VARIABLE_ONE -> $(VARIABLE_ONE)"
	echo "VARIABLE_TWO -> $(VARIABLE_TWO)"
```


Check that no configuration files already exist...


```bash
ls -1a "${PWD}"
#> .
#> ..
#> Makefile
```


Print `make` variables...


```bash
make debug
#> VARIABLE_ONE -> first default
#> VARIABLE_TWO -> second default
```


Generate a configuration file, and confirm that configuration file was written...


```bash
make config

ls -1a "${PWD}"
#> .
#> ..
#> .make-config
#> Makefile
```


Edit the configuration file, and confirm `make` variables where modified...


```bash
sed -i '{
  /ONE/ s#= .*#= first modified#;
  /TWO/ s#= .*#= second modified#;
}' config

make debug
#> VARIABLE_ONE -> first modified
#> VARIABLE_TWO -> second modified
```


Remove the configuration file...


```bash
make clean

ls -1a "${PWD}"
#> .
#> ..
#> Makefile
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

