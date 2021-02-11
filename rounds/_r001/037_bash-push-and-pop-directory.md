---
layout: post
title: Bash Push and Pop Directory
date: 2021-02-10 20:07:59 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Scripting and interactive shell trick for changing current working directory
time_to_live: 1800
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

