---
layout: post
title: Makefile Target Chaining
date: 2021-04-08 15:54:33 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to execute ordered, and unordained, list(s) of make targets
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://twitter.com/S0_And_S0/status/1380294199904403456
  title: Link to Tweet for this post
---



One of the key features I've come to really appreciate about Make files is listing steps in either a parallel or ordered list...


**Ordered Syntax**


```make
ordered-targets: | target-one target-two target-three
```


**Parallel Syntax**


```make
parallel-targets: step-one step-two step-three
```


In the case of an ordered list, denoted by the vertical bar (`|`), steps will be preformed synchronously in the order listed, and by default an error state from any step will halt execution.


In the case of a parallel list, steps will be preformed in a multi-threaded fashion, which can be super helpful for improving performance.


Furthermore combination of parallel and ordered lists can further improve installation times, eg...


**`Makefile` (snip)**


```make
install: | download-dependencies build-dependencies compile link

download-dependencies: download-dep-one download-dep-two download-dep-three

build-dependencies: build-dep-one build-dep-two build-dep-three

complie:
	echo "compile target not implemented!"
	exit 1

link:
	echo "link target not implemented!"
	exit 1
```


... in above example the `download-dependencies` and `build-dependencies` targets will preform actions multi-threaded, but the `install` target will wait for each to finish without error before attempting to execute the next step.


> Note, depending upon device configurations the `-j` option with a number may be necessary when running make commands to preform multi-threaded actions, eg...
>
>     make -j4 install
>
> ... would allow Make to utilize up to four threads.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

