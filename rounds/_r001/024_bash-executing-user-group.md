---
layout: post
title: Bash Executing User Group
date: 2021-01-28 20:29:36 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to get user/group executing `sudo` within Bash script
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Quick script example of how to get user/group executing `sudo` within Bash script...


**`executing-user-group.sh`**


```bash
#!/usr/bin/env bash

_executing_user="${SUDO_USER:-${USER}}"
_executing_group="${GROUPS}"
[[ "${_executing_user}" != 'root' ]] && {
    _executing_group="$(groups "${_executing_user}" | awk '{print $3}')"
}

printf '_executing_user -> %s\n' "${_executing_user}"
printf '_executing_group -> %s\n' "${_executing_group}"
```


**Example Usage**


```bash
sudo ./executing-user-group.sh
#> _executing_user -> s0ands0
#> _executing_group -> s0ands0
```


... I've found this to be super useful within scripts that write files from `root` but where executed as a normal account. For example the [`paranoid-linu/script-apt-get`][link__paranoid_linux__script_apt_get] project utilizes this trick to write logs to the executing user's `home` directory and re-assign file ownership.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__paranoid_linux__script_apt_get]: https://github.com/paranoid-linux/script-apt-get "Logs `install` and `upgrade` actions for `apt-get` via `script`"

