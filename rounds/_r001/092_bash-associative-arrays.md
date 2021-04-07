---
layout: post
title: Bash Associative Arrays
date: 2021-04-06 16:55:31 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Tips and tricks for assigning and parsing associative arrays in Bash
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://example.com
  title: Link to Tweet for this post
---



One of the features of Bash that I do not see often utilized are associative arrays, which operate similar to one-dimensional dictionaries.


Here's a quick example of how to declare and assign elements to an associative array...


```bash
declare -A example_one=(
  ['key_one']='value one'
  ['key_two']='value two'
)

example_one['key_three']=3
```


... and an example of enumerating key value pares...


```bash
for _key in "${!example_one[@]}"; do
  printf '%s -> %s\n' "${_key}" "${example_one[${_key}]}"
done
```


> Note, the `!` prefix to either associative or indexed arrays will list keys or indexes.


---


Taking this a step further it is possible to use associative arrays to define defaults that may be overridden, eg...


**`associative-array-example.sh`**


```bash
#!/usr/bin/env bash


parse_associative_array() {
    local -n _defaults="${1}"
    local -n _options="${2}"

    local _key _option_value _default_value _value
    for _key in "${!_defaults[@]}"; do
        _default_value="${_defaults[${_key}]}"
        _option_value="${_options[${_key}]}"
        _value="${_option_value:-${_default_value}}"

        declare -g "${_key//-/_}=${_value}"

        unset _option_value
        unset _default_value
        unset _value
    done
    unset _key
}


# shellcheck disable=SC2034
declare -A DEFAULTS=(
    ['--param-one']='canned ham'
    ['--param-two']='fresh spam'
)

# shellcheck disable=SC2034
declare -A OPTIONS=(
    ['--param-one']='jello pocket'
)

parse_associative_array DEFAULTS OPTIONS


# shellcheck disable=SC2154
{
    printf '# --param-one -> __param_one => %s\n' "${__param_one}"
    printf '# --param-two -> __param_two => %s\n' "${__param_two}"
}
```


**Notes**


- the `-n` option of `local -n` allows for passing a variable by reference, which is the only way I've found to pass more than one array to a function

- the `-A` option of `declare -A` assigns/initializes an associative array

- the `-g` option of `declare -g` assigns a variable to the global/script scope

- the `:-` portion of `_value="${_option_value:-${_default_value}}"` will assign `_value` to `${_default_value}` if `${_option_value}` is undefined

- the `//-/_` portion of `declare -g "${_key//-/_}=${_value}"` is a Bash builtin that will replace all instances of `-` with `_`

- `unset` will _delete_ a variable


**Documentation**


- `help declare`

- `help local`

- `help unset`

- `man --pager='less --pattern="^\s+Parameter Expansion"' bash`


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

