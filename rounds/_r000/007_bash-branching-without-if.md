---
layout: post
title: Bash Branching Without If
date: 2020-05-04 10:10:35 -0700
#date_updated:  # Optional and formatted like 'date' above
description: "`if`, `then`, and `fi` can be optional when `elif` is not used"
time_to_live: 1800
category: bash
---



In Bash scripting `if`, `then`, and `fi` can be optional when `elif` isn't used...


```bash
_file_path="/tmp/somewhere.ext"

[[ -f "${_file_path}" ]] && {
  printf 'Found -> %s\n' "${_file_path}"
} || {
  printf 'Cannot read -> %s\n' "${_file_path}"
}
```


... above is equivalent to...


```bash
_file_path="/tmp/somewhere.ext"

if [[ -f "${_file_path}" ]]; then
  printf 'Found -> %s\n' "${_file_path}"
else
  printf 'Cannot read -> %s\n' "${_file_path}"
fi
```


... and can be nested or chained like slandered `if` branching


```bash
path_walker() {
  local _path="${1%%*(//|/)}"

  (("${#_path}")) && [[ -f "${_path}" ]] && {
    printf 'Found -> %s\n' "${_path}"
  } || {
    [[ -d "${_path}" ]] && {
      printf 'Is a directory -> %s\n' "${_path}"
      while read -r _sub_path; do
        (("${#_sub_path}")) && {
          path_walker "${_path}/${_sub_path}"
        }
      done <<<"$(ls "${_path}")"
    }
  }
}

path_walker "/tmp/somewhere.ext"
```


... above is similar, though likely less readable in comparison to...


```bash
path_walker() {
  local _path="${1%%*(//|/)}"

  if (("${#_path}")) && [[ -f "${_path}" ]]; then
    printf 'Found -> %s\n' "${_path}"
  elif [[ -d "${_path}" ]]; then
    printf 'Is a directory -> %s\n' "${_path}"
    while read -r _sub_path; do
      if (("${#_sub_path}")); then
        path_walker "${_path}/${_sub_path}"
      fi
    done <<<"$(ls "${_path}")"
  fi
}

path_walker "/tmp/somewhere.ext"
```


... sometimes it'll read better to have `if` and `fi` for branching, other times it's simpler to read/write with logical operators and curly braces.
