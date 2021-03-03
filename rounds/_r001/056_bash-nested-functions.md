---
layout: post
title: Bash Nested Functions
date: 2021-03-01 15:15:04 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Tips and gotchas for assigning and using nested Bash functions
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1366528636216631296
  title: Link to Tweet for this post
---


In other functional languages, such as JavaScript, it's common to have functions within functions, and while Bash does not expressly forbid it there are some subtle differences.


Consider the following script example...


**`example-one.sh`**


```bash
#!/usr/bin/env bash


mutate() {
    printf 'This should not be called by bellow function(s)\n'
}


name_space() {
    local -n _shared_array_reference="${1:?No array reference provided}"

    mutate() {
        for i in {1..10}; do
            _shared_array_reference+=( "$((i * 2))" )
        done
    }

    mutate
}


mutable_array=(1 2 3)
name_space mutable_array

for i in "${!mutable_array[@]}"; do
    printf 'mutable_array[%i] -> %s\n' "${i}" "${mutable_array[$i]}"
done
```


... At first one may believe the above is okay, however, the `mutate` function within `name_space` will overwrite the _outer-scoped_ `mutate` function!


There is another option though and that is defining a sub-shell function, by replacing curly braces (`{` and `}`) after `name_space` with parentheses (`(` and `)`), eg...


**`example-two.sh`**


```bash
#!/usr/bin/env bash


mutate() {
    local -n _array_reference="${1:?No array reference provided}"
    for i in {1..10}; do
        _array_reference+=( "$((i * 2))" )
    done
}


name_space() (
    local -n _shared_array_reference="${1:?No array reference provided}"

    mutate() {
        for i in {1..10}; do
            _shared_array_reference+=( "$((i * 2))" )
        done
    }

    mutate
)


mutable_array=(1 2 3)
name_space mutable_array

for i in "${!mutable_array[@]}"; do
    printf 'mutable_array[%i] -> %s\n' "${i}" "${mutable_array[$i]}"
done
```


... While this does prevent the script-level `mutate` function from being overwritten by `name_space`, output of `example-one.sh` and `example-two.sh` scripts will be significantly different!


**Output of `example-one.sh`**


```text
mutable_array[0] -> 1
mutable_array[1] -> 2
mutable_array[2] -> 3
mutable_array[3] -> 2
mutable_array[4] -> 4
mutable_array[5] -> 6
mutable_array[6] -> 8
mutable_array[7] -> 10
mutable_array[8] -> 12
mutable_array[9] -> 14
mutable_array[10] -> 16
mutable_array[11] -> 18
mutable_array[12] -> 20
```


**Output of `example-two.sh`**


```text
mutable_array[0] -> 1
mutable_array[1] -> 2
mutable_array[2] -> 3
```


Initially I thought this behaviour to be somewhat limiting, but recently I've come to understand that there are some valid use-cases. For example suppose that a script should define a function only if not already defined, eg...


**`main.sh`**


```bash
#!/usr/bin/env bash

source 'lib/overwrites.sh'

something() {
    printf 'Some thing!\n'
}


if type otherthing 2>/dev/null | head -n1 | grep -qE 'function$'; then
    overwrites
fi

something
otherthing
```


**`lib/overwrites.sh`**


```bash
#!/usr/bin/env bash


overwrites() {
    otherthing() {
        printf 'Other thing!\n'
    }
}
```


... Where `otherthing` defined by the shell or some script that imported `main.sh`, the `overwrites` function would never be called!


And of course the _sub-shell_ syntax for nesting functions is useful for making name-spaces that do not overwrite functions, or variables, within the outer-scope. However because execution is within a sub-shell, one must take care to produce output and/or exit status codes that are useful to the outer-scope.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

