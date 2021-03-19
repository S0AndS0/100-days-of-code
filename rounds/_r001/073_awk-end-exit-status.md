---
layout: post
title: Awk End Exit Status
date: 2021-03-18 14:15:51 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Gotcha of Awk exit status being concealed by END block(s)
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1372658956259233794
  title: Link to Tweet for this post
---



Awk, or more specifics GAwk, has five sections/blocks to organize execution...


```awk
#!/usr/bin/awk -f

BEGIN {}

BEGINFILE {}

{}

ENDFILE {}

END {}
```


- _`BEGIN`_ block runs prior to reading **any** file inputs

- _`BEGINFILE`_ block runs before each file input

- _`{}`_ block runs for each line read from **all** file inputs

- _`ENDFILE`_ block runs after each file input

- _`END`_ block runs after **all** file inputs


> Note, as of writing this post _classic_ Awk does **not** have _`BEGINFILE`_, or _`ENDFILE`_, code blocks


For one of my most recent projects I wanted to exit prematurely from parsing, as well as use the exit status for branching logic. Following is a simplified example...


**`find-after.sh`**


```bash
#!/usr/bin/env bash

_file="${1:?No file provided!}"
_pattern="${2:?No pattern provided}"
_section="${3:?No section provided}"

if awk -v _pattern="${_pattern}" -v _section="${_section}" '
BEGIN {
    _after_section = 0;
}

{
    if (_after_section && $0 ~ _pattern) {
        exit 1;
    } else if ($0 == _section) {
        _after_section = 1;
    }
}' "${_file}"
then
    echo 'Found pattern!'
else
    echo 'Did not find it'
fi
```


... which _should_ function as intended, eg...


```bash
find-after.sh 'test.txt' 'pattern' 'section'
```


... _should_ report if _`pattern`_ is found after _`section`_ within file _`test.txt`_, or not.


---


Where issues arise is when Awk contains an _`ENDFILE`_, or _`END`_, code blocks. Because these blocks are executed regardless of the _main_ _`{}`_ parsing loop!


**`awk-exit-example-one.sh`**


```bash
#!/usr/bin/env bash

awk '{
    if ($0 == 1) {
        exit 1;
    }
    exit 0;
}

END {
    print "Reached END block";
}' <<< "${1:-0}"

_exit_status="${?}"
printf 'Exit status -> %i\n' "${_exit_status}"
```


Example output of `awk-exit-example-one.sh`...


```bash
awk-exit-example-one.sh 1
#> Exit status -> 0

awk-exit-example-one.sh 0
#> Exit status -> 0
```


Currently the way I've worked around this _`Awk`ward_ behaviour is by setting a variable and checking that state prior to exiting from an _`END`_ block, eg...


**`awk-exit-example-two.sh`**


```bash
#!/usr/bin/env bash

awk 'BEGIN {
    _exit_state = 0;
}
{
    if ($0 == 1) {
        _exit_state = 1;
        exit 1;
    }
    exit 0;
}

END {
    print "Reached END block";

    if (_exit_state) {
        exit _exit_state;
    }
}' <<< "${1:-0}"

_exit_status="${?}"
printf 'Exit status -> %i\n' "${_exit_status}"
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

