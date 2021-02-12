---
layout: post
title: Bash Push and Pop Directory
date: 2021-02-10 20:07:59 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Scripting and interactive shell trick for changing current working directory
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1359724832284413954
  title: Link to Tweet for this post
---



When writing Bash scripts and while operating within the interactive shell, I often change the current working directory, do some operation(s), then revert current working directory back.


Example workflow...


```bash
mkdir some/where

cd some/where

touch file.ext

cd ../..
```


However, there are builtin commands that reduce the chances of mistakes when reverting current working directory.


Enhanced workflow example...


```bash
mkdir some/where

pushd some/where

touch file.ext

popd
```


The `pushd` and `popd` commands are _magical_ when writing scripts too, eg...


**`bulk-git-add.sh`**


```bash
#!/usr/bin/env bash


set -Ee

_file_name='file.ext'

_directory_list=(
  'some/where'
  'another/plane'
  'elsewhere'
)


for _directory in "${_directory_list[@]}"; do
  pushd "${_directory}"

  if [[ -f "${_file_name}" ]]; then
    git add "${_file_name}"
    git commit -m "Adds ${_file_name} to version control"
  fi

  popd
done
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

