---
layout: post
title: Bash Multi-Line Variables
date: 2020-05-02 11:09:37 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Assigning and appending to multi-line variable with Bash
time_to_live: 1800
category: bash
---


Assigning and appending to multi-line variable with Bash...


```bash
read -r -d '' _variable_name <<EOF
first
second
EOF


read -r -d '' _variable_name <<EOF
${_variable_name}
third
EOF

printf '%s\n' "${_variable_name}"
#> first
#> second
#> third
```


One caveat with this method is that `traps` when combined with certain `set` configurations may trip even though there was no reported error code, so any failure trapping functions should filter for non-zero exit status, eg...


```bash
#!/usr/bin/env bash
set -E -o functrace


failure(){
    local -n _lineno="${1:-LINENO}"
    local -n _bash_lineno="${2:-BASH_LINENO}"
    local _last_command="${3:-${BASH_COMMAND}}"
    local _code="${4:-0}"

    ## Workaround for read EOF combo tripping traps
    ((_code)) || {
      return "${_code}"
    }

    printf '%i:%i -> %s' "${_lineno}" "${_bash_lineno}" "${_last_command}"
    exit "${_code}"
}

trap 'failure "LINENO" "BASH_LINENO" "${BASH_COMMAND}" "${?}"' ERR


read -r -d '' _variable_name <<EOF
first
second
EOF


read -r -d '' _variable_name <<EOF
${_variable_name}
third
EOF

printf '%s\n' "${_variable_name}"
```
