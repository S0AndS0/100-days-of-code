---
layout: post
title: Three code publishing tips
date: 2020-06-27 09:45:22 -0700
#date_updated:  # Optional and formatted like Sat Jun 27 09:45:22 PDT 2020 above
description: Examples of how to separate the responsibilities of a project
time_to_live: 1800
---



These are examples from a _live_ project, built from many years of Open Source publishing experience, and the aim to demonstrate how to separate the responsibilities of a project.


------


- [Code Answers "What?"][heading__code_answers_what]

- [Comments Answer "Why?"][heading__comments_answer_why]

- [Documentation Answers "How?"][heading__documentation_answers_how]

- [Notes][heading__notes]


------



## Code Answers "What?"
[heading__code_answers_what]: #code-answers-what "Eg. _what_ should be done"


_What_ should be done, _what_ data or parameters are needed or parsed, etc.


[**`failure.sh`**][github__trap_failure_failure_sh]


```bash
#!/usr/bin/env bash


# Bash Trap Failure, a submodule for other Bash scripts tracked by Git
# Copyright (C) 2019  S0AndS0
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU Affero General Public License as published
# by the Free Software Foundation; version 3 of the License.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU Affero General Public License for more details.
#
# You should have received a copy of the GNU Affero General Public License
# along with this program.  If not, see <https://www.gnu.org/licenses/>.


## Outputs Front-Mater formatted failures for functions not returning 0
## Use the following line after sourcing this file to set failure trap
##    trap 'failure "LINENO" "BASH_LINENO" "${BASH_COMMAND}" "${?}"' ERR
failure(){
    local -n _lineno="${1:-LINENO}"
    local -n _bash_lineno="${2:-BASH_LINENO}"
    local _last_command="${3:-${BASH_COMMAND}}"
    local _code="${4:-0}"

    ## Workaround for read EOF combo tripping traps
    ((_code)) || {
      return "${_code}"
    }

    local _last_command_height="$(wc -l <<<"${_last_command}")"

    local -a _output_array=()
    _output_array+=(
        '---'
        "lines_history: [${_lineno} ${_bash_lineno[*]}]"
        "function_trace: [${FUNCNAME[*]}]"
        "exit_code: ${_code}"
    )

    [[ "${#BASH_SOURCE[@]}" -gt '1' ]] && {
        _output_array+=('source_trace:')
        for _item in "${BASH_SOURCE[@]}"; do
            _output_array+=("  - ${_item}")
        done
    } || {
        _output_array+=("source_trace: [${BASH_SOURCE[*]}]")
    }

    [[ "${_last_command_height}" -gt '1' ]] && {
        _output_array+=(
            'last_command: ->'
            "${_last_command}"
        )
    } || {
        _output_array+=("last_command: ${_last_command}")
    }

    _output_array+=('---')
    printf '%s\n' "${_output_array[@]}" >&2
    exit ${_code}
}
```


> Note, aside from license and small usage example, the only other comment is a _hint_ as to _why_ some bit of questionable code exists.


___


## Comments Answer "Why?"
[heading__comments_answer_why]: #comments-answer-why "Eg. _why_ a questionable bit of code exists"


_Why_ a questionable bit of code exists, _why_ something it written the way it is, etc.


[**`failure.sh`** (snip lines 29-32)](https://github.com/bash-utilities/trap-failure/blob/v0.0.2/failure.sh#L29-L32)


```bash
    ## Workaround for read EOF combo tripping traps
    ((_code)) || {
      return "${_code}"
    }
```


The comment text _`## Workaround for read EOF combo tripping traps`_ refers to an odd gotcha involving traps and `read` with `EOF` (here-doc) markers. For example something like...


```bash
read -rd '' _variable <<'EOF'
line one
second line
line three
EOF
```


... will trip some traps even though the return/exit code is `0` (not an error), which is _why_ the `failure` function checks if the exit `_code` is really an error code.


___


## Documentation Answers "How?"
[heading__documentation_answers_how]: #documentation-answers-how "Eg. _how_ to utilize the code..."


_How_ to utilize the code, _how_ to download, _how_ to contribute, etc.


**[`ReadMe.md` (snip from `master` branch)][github__trap_failure__master__readme_md]**


> ## Installation
>
>
> Add one of the available clone URLs to a current project...


```bash
cd your-project

_url='https://github.com/bash-utilities/trap-failure.git'
_dir='modules/trap-failure'

git submodule add -b master "${_url}" "${_dir}"
```


> ...


**[`ReadMe.md` (snip from `example` branch)][github__trap_failure__example__readme_md]**


> The key takeaways from the above script are...


```Bash
set -E -o functrace
source "${__DIR__}/modules/trap-failure/failure.sh"
trap 'failure "LINENO" "BASH_LINENO" "${BASH_COMMAND}" "${?}"' ERR
```


> - The `set` line allows for one more layer of tracing what tripped the trap within the line number list
>
> - The `source` line pulls the `failure` function into the same scope as the example usage script
>
> ...


___


## Notes
[heading__notes]: #notes "Additional notable bits and/or takeaways"


These examples are intended as _guidelines_ **not** _rules_; ie. bend/break them when necessary. Some language, such as Python and Rust, have the concept of _doc. strings_ or _doc. comments_, and in such cases these generally should answer _"how"_ to utilize a specific function, class, etc.


**Takeaways**


- When code focuses on answering [_"what?"_][heading__code_answers_what] it is often more readable and easier to maintain.


- When comments focus on answering [_"why?"_][heading__comments_answer_why] they're generally more concise and less likely to be ignored.


- When documentation focuses on answering [_"how?"_][heading__documentation_answers_how] it can make utilization faster for both those new, and returning, to a project.



[github__trap_failure_failure_sh]: https://github.com/bash-utilities/trap-failure/blob/v0.0.2/failure.sh "Source code from `bash-utilities/trap-failure` repository"

[github__trap_failure__example__readme_md]: https://github.com/bash-utilities/trap-failure/blob/d0.0.2/README.md "Documentation for example usage of `bash-utilities/trap-failure` repository"

[github__trap_failure__master__readme_md]: https://github.com/bash-utilities/trap-failure/blob/v0.0.2/README.md "Documentation of `bash-utilities/trap-failure` repository"
