# 100 Days of Code
[heading__top]:
  #100-days-of-code
  "&#x2B06; Compilation of code tips and tricks over specified time period"


Compilation of code tips and tricks over specified time period


## [![Byte size of 100 Days Of Code][badge__gh_pages__100_days_of_code__source_code]][100_days_of_code__gh_pages__source_code] [![Open Issues][badge__issues__100_days_of_code]][issues__100_days_of_code] [![Open Pull Requests][badge__pull_requests__100_days_of_code]][pull_requests__100_days_of_code] [![Latest commits][badge__commits__100_days_of_code__gh_pages]][commits__100_days_of_code__gh_pages] [![100-days-of-code Demos][badge__gh_pages__100_days_of_code]][gh_pages__100_days_of_code]



------


- [:arrow_up: Top of Document][heading__top]

- [:building_construction: Requirements][heading__requirements]

- [&#x1F5D2; Notes][heading__notes]

- [:card_index: Attribution][heading__attribution]

- [:balance_scale: Licensing][heading__license]


------



## Requirements
[heading__requirements]:
  #requirements
  "&#x1F3D7; Prerequisites and/or dependencies that this project needs to function properly"


This repository makes use of Git Submodules to track dependencies, to avoid incomplete downloads clone with the `--recurse-submodules` option...


```Bash
git clone --recurse-submodules git@github.com:S0AndS0/100-days-of-code.git
```


To update tracked Git Submodules issue the following commands...


```Bash
git pull

git submodule update --init --merge --recursive
```


To force upgrade of Git Submodules...


```Bash
git submodule update --init --merge --recursive --remote
```


> Note, forcing and update of Git Submodule tracked dependencies may cause instabilities and/or merge conflicts; if however everything operates as expected after an update please consider submitting a Pull Request.


___



## Notes
[heading__notes]:
  #notes
  "&#x1F5D2; Additional things to keep in mind when developing"


This repository is built with the help of [Jekyll](https://jekyllrb.com), served with thanks to [GitHub Pages](https://pages.github.com), and available at [`https://S0AndS0.github.io/100-days-of-code`](https://S0AndS0.github.io/100-days-of-code)


Private testing is facilitated by [Jekyll_Admin](https://github.com/S0AndS0/Jekyll_Admin), though not necessarily required.


Pull Requests that correct mistakes/bugs, or add features are certainly welcomed.


___


## Attribution
[heading__attribution]:
  #attribution
  "&#x1F4C7; Resources that where helpful in building this project so far."


- [GitHub -- `github-utilities/make-readme`](https://github.com/github-utilities/make-readme)


___


## License
[heading__license]:
  #license
  "&#x2696; Legal side of Open Source"


```
Compilation of code tips and tricks over specified time period
Copyright (C) 2020 S0AndS0

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, version 3 of the License.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

```


For further details review full length version of [AGPL-3.0][branch__current__license] License.



[branch__current__license]:
  /LICENSE
  "&#x2696; Full length version of AGPL-3.0 License"


[badge__commits__100_days_of_code__gh_pages]:
  https://img.shields.io/github/last-commit/S0AndS0/100-days-of-code/gh-pages.svg

[commits__100_days_of_code__gh_pages]:
  https://github.com/S0AndS0/100-days-of-code/commits/gh-pages
  "&#x1F4DD; History of changes on this branch"


[100_days_of_code__community]:
  https://github.com/S0AndS0/100-days-of-code/community
  "&#x1F331; Dedicated to functioning code"

[100_days_of_code__gh_pages]:
  https://github.com/S0AndS0/100-days-of-code/tree/
  "Source code examples hosted thanks to GitHub Pages!"

[badge__gh_pages__100_days_of_code]:
  https://img.shields.io/website/https/S0AndS0.github.io/100-days-of-code/index.html.svg?down_color=darkorange&down_message=Offline&label=Demo&logo=Demo%20Site&up_color=success&up_message=Online

[gh_pages__100_days_of_code]:
  https://S0AndS0.github.io/100-days-of-code/index.html
  "&#x1F52C; Check the example collection tests"

[issues__100_days_of_code]:
  https://github.com/S0AndS0/100-days-of-code/issues
  "&#x2622; Search for and _bump_ existing issues or open new issues for project maintainer to address."

[pull_requests__100_days_of_code]:
  https://github.com/S0AndS0/100-days-of-code/pulls
  "&#x1F3D7; Pull Request friendly, though please check the Community guidelines"

[100_days_of_code__gh_pages__source_code]:
  https://github.com/S0AndS0/100-days-of-code/
  "&#x2328; Project source!"

[badge__issues__100_days_of_code]:
  https://img.shields.io/github/issues/S0AndS0/100-days-of-code.svg

[badge__pull_requests__100_days_of_code]:
  https://img.shields.io/github/issues-pr/S0AndS0/100-days-of-code.svg

[badge__gh_pages__100_days_of_code__source_code]:
  https://img.shields.io/github/repo-size/S0AndS0/100-days-of-code
