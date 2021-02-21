---
layout: post
title: Git Ignore Defaults
date: 2021-02-20 17:00:28 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Git tips for defining default ignore patters for all repositories
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1363296124740792320
  title: Link to Tweet for this post
---



Those that have utilized Git for awhile may have on occasion added, committed, and may be even pushed directories or files that should not be included within a repository. Many that are experienced with Git may define a `.gitignore` file per-repository, and that works well most of the time. However, when initializing a new repository there are no such safe-guards by default.


At the time of writing there are two methods that can mitigate issues of tracking files that should otherwise be ignored.


---


- [Option One][heading__option_one]

- [Option Two][heading__option_two]

- [Caveats][heading__caveats]

- [Attribution][heading__attribution]

- [Contact and/or Contribute][heading__contact_andor_contribute]


---



## Option One
[heading__option_one]: #option-one "Define an account `ignore` file for Git"


Define an account `ignore` file for Git...


```bash
mkdir -p "${HOME}/.config/git"

tee -a "${HOME}/.config/git/ignore" <<'EOF'
node_modules
*.swp
EOF
```


... above is useful for patterns that are common among most, if not all, repositories that an account maintains.


______


## Option Two
[heading__option_two]: #option-two "Configure a Git template directory and customize the `info/exclude` file"


Configure a Git template directory and customize the `info/exclude` file...


```bash
mkdir -p "${HOME}/.config/git/templates"

cp -r /usr/share/git-core/templates "${HOME}/.config/git/templates/default"

tee -a "${HOME}/.config/git/templates/default/info/exclude" <<'EOF'
*.swp
EOF

git config --global init.templateDir "${HOME}/.config/git/templates/default"
```


... above is useful for patterns that are common in some, but not all, repositories that an account maintains.i


For example other templates may be defined for specific uses.


**NPM specific template**


```bash
mkdir -p "${HOME}/.config/git/templates"

cp -r "${HOME}/.config/git/templates/default" "${HOME}/.config/git/templates/npm"

tee -a "${HOME}/.config/git/templates/npm/info/exclude" <<'EOF'
node_modules
EOF
```


Selecting a specific template...


```bash
git init --template=~/.config/git/templates/npm\
         new-project-name
```


______


## Caveats
[heading__caveats]: #caveats "Things to keep in mind when defining default Git ignore patterns"


Beware, when defining default Git ignore patterns via either of above options it is still possible to add and commit files that should be ignored. Either via `--force` option...


```bash
git add --force some-ignored-file
```


... or because of a contributor that does not have the same default configurations.


This is because nether the `.git/info/exclude`, or `~/.config/git/ignore`, files are tracked by an individual Git repository. So while account/template based Git ignore files are useful, it is still a very good idea to utilize a repository level `.gitignore` file; especially when a repository is shared with other contributors.


For example sharing defined defaults from a template may be achieved via...


```bash
git init some-project

cd some-project

grep -v '#' "${PWD}.git/info/exclude" >> .gitignore
```


______


## Attribution
[heading__attribution]: #attribution "Resources that where helpful in writing this post"


Relevant documentation may be reviewed via...


```bash
git help ignore

man --pager='less --pattern="^TEMPLATE"' git-init
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

