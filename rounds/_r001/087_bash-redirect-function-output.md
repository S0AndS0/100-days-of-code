---
layout: post
title: Bash Redirect Function Output
date: 2021-04-01 16:07:45 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to redirect output of a Bash function automatically
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://example.com
  title: Link to Tweet for this post
---


Within some of my Bash script I'll on occasion want to format output send to STDERR (Standered Error), which may be written as something like...


```bash
format_error() {
  local _header="${1}"

  shift
  local _lines=( "${@}" )

  printf >&2 '%s\n' "${_header}"
  printf >&2 '  %s\n' "${_lines[@]}"
}
```


... However, I recently learned the repeaded `>&2` redirection was redundent, because the whole block of commands may be sent to STDERR via code similar to...


```bash
format_error() {
  local _header="${1}"

  shift
  local _lines=( "${@}" )

  printf '%s\n' "${_header}"
  printf '  %s\n' "${_lines[@]}"
} >&2
```


What's more is that this trick may be used for writing/appending output to files too!


**`log_message.sh`**


```bash
#!/usr/bin/env bash


_log_file="${1?No log file path provided}"
shift
_message_lines=( "${@}" )


log_message() {
    local -n _lines="${1}"
    if ! (( "${#_lines}" )); then
        return
    fi

    local _time_stamp
    _time_stamp="$(date +'%Y-%m-%d_%H:%M:%S')"

    printf '%s\n' "${_time_stamp}"
    printf '  %s\n' "${_lines[@]}"
} >> "${_log_file}"


log_message '_message_lines'
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__100_days_of_code__r001_084__vim_glob]: {{ r001/084-vim-glob | absolute_url }} "Using glob function to source vim configurations from sub-directories"

