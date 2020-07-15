---
layout: post
title: Git hooks on push
date: 2020-05-31 11:39:12 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Bash script that runs Git hooks on push
time_to_live: 1800
---



Bash script that runs Git hooks on push...


**`~/bin/git-push-wh`**


```bash
#!/usr/bin/env bash

_git_hooks_dir="${PWD}/.git/hooks"
_pre_push="${_git_hooks_dir}/pre-push"
_post_push="${_git_hooks_dir}/post-push"

[[ -e "${_pre_push}" ]] && {
  "${_pre_push}" "${@}"
}

git push "${@}"

[[ -e "${_post_push}" ]] && {
  "${_post_push}" "${@}"
}
```


Example usage...


```bash
cd project-directory

git-push-wh origin master
```


Provided that the project has scripts under `.git/hooks` named `pre-push` and/or `post-push` that are executable, the above script will call'em at the proper time.
