---
layout: post
title: Bash Error Traps
date: 2021-02-11 16:03:58 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Introduction to handling errors in Bash scripts
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1360031073028235265
  title: Link to Tweet for this post
---



Bash, unlike other scripting languages, does **not** halt on errors by default. However, it is possible to opt-in to such functionality via `set` command, eg...


```bash
#!/usr/bin/env bash

set -eE

# ... commands or functions that may error ... #
```


Bash also does not have `try`/`catch` keywords, however, there are ways to achive similar functionality via the `trap` command, and assigning a _catch_ function, eg...


```bash
#!/usr/bin/env bash


set -eE


catch() {
  local _exit_status="${1}"
  local _last_command="${2}"

  (( _exit_status )) || {
    return "${_exit_status}"
  }

  printf >&2 'Failed to run -> %s\n' "${_last_command}"
  exit "${_exit_status}"
}


trap 'catch "${?}" "${BASH_COMMAND}"'


# ... commands or functions that may error ... #
```


Further information about shell builtin commands and variables are accessible via;


- `help set`

- `help trap`

- `man --pager='less --pattern "^\s+Shell Variables"' bash`


A ready to use Bash error parsing module can be cloned from [GitHub `bash-utilities/trap-failure`][link__bash_utilities__trap_failure], and included within any Bash script via `source` command.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__bash_utilities__trap_failure]: https://github.com/bash-utilities/trap-failure

