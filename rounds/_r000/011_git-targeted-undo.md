---
layout: post
title: Git Targeted Undo
date: 2020-05-08 09:20:13 -0700
#date_updated:  # Optional and formatted like Fri May  8 09:20:13 PDT 2020 above
description: Turning back time with Git
time_to_live: 1800
---



**Turning back time with Git**


- Obtain commit hash for three commits ago...


```bash
_past_ref_hash="$(git log --oneline | awk 'NR == 3 { print $1; exit 0; }')"
```


> `git log --oneline` will print commit reference hashes at the beginning of each line, then the first line of each message
> Awk `NR == 3` targets the third line of piped input
> Awk `print $1` prints the first _word_ of matched input
> and Awk `exit 0` stops searching piped input


------


- Checkout committed state, then a new _`fix`_ branch for tracking changes...


```bash
git checkout "${_past_ref_hash}"
git checkout -b fix
```


> Checking out a new branch named `fix` with `-b fix` re-attaches the `HEAD`, and enables new commits to be made without effecting the `master` branch; hint try `git status` prior to review the repository state when a commit ref has been checked-out.


------


- Make fixes then commit changes to _`fix`_ branch...


```bash
git commit -m 'Fixes something'
```


> While the _`fix`_ branch is checked out it's okay, and generally encouraged to make lots of commits.


------


- Checkout the source branch, _`master`_ in this example, and merge _`fix`_ changes in...


```bash
git checkout master
git merge fix
```


> Note, if multiple commit messages where made on the _`fix`_ branch, then...
> `git merge --squash fix`
> ... allows for writing a new message that covers all changes being merged into the _`master`_ branch.


------


- Clean-up by deleting _`fix`_ branch when done...


```bash
git branch --delete fix
```


> **Do not** delete the _`fix`_ branch until totally satisfied with changes.
