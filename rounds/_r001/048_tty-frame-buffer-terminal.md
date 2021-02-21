---
layout: post
title: TTY Frame Buffer Terminal
date: 2021-02-21 11:11:50 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Guide on how to enable full color support within TTY terminal sessions
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post

attribution:
  links:
    - text: Ask Ubuntu -- How do I set up a background image for console
      href: https://askubuntu.com/questions/278863/
      title: How do I set up a background image for console
      class: fa fa-stack-exchange

    - text: StackOverflow -- List of ANSI color escape sequences
      href: https://stackoverflow.com/questions/4842424/
      title: List of ANSI color escape sequences
      class: fa fa-stack-overflow
---



Personally I find operating on TTY sessions to be a distraction free experience, however, I also like having syntax highlighting within Vim and other terminal applications. So this here is a guide on how to enable full color support within TTY terminal sessions


---


- [Install `fbterm`][heading__install_fbterm]

- [Restrict `setuid` permissions][heading__restrict_setuid_permissions]

- [Add Account to `video` Group][heading__add_account_to_video_group]

- [Edit `~/.bashrc`][heading__edit_bashrc]

- [Edit `~/.profile`][heading__edit_profile]

- [Usage][heading__usage]

- [Contact and/or Contribute][heading__contact_andor_contribute]

- [Attribution](#heading__attribution)


---



## Install `fbterm`
[heading__install_fbterm]: #install-fbterm


```bash
sudo apt-get update

sudo apt-get install fbterm
```


______



## Restrict `setuid` permissions
[heading__restrict_setuid_permissions]: #restrict-setuid-permissions



```bash
sudo setcap 'cap_sys_tty_config+ep' "$(which fbterm)"
```


> Note, check the manual entry for more details about above
>
>     man --pager='less -p "^SECURITY NOTES"' fbterm


______


## Add Account to `video` Group
[heading__add_account_to_video_group]: #add-account-to-video-group


Add current account to `video` group, which _should_ allow for background images to be displayed within console


```bash
sudo usermod -a -G video ${USER}
```


______


## Edit `~/.bashrc`
[heading__edit_bashrc]: #edit-bashrc


**`~/.bashrc` (snip)**


```bash
##
# fbterm and screen/tmux customization for TTY/GUI terminals
# See: ~/.profile
if (( FBTERM )) && [[ -e "$(which fbterm)" ]]; then
  if [[ "${TERM}" =~ ^'screen' ]]; then
    export TERM=screen-256color
  else
    export TERM=fbterm
  fi
elif [[ "${TERM}" =~ ^'screen' ]]; then
  export TERM=screen-256color
fi
```


> The above configurations ensure the `TERM` environment variable is configured correctly for most combinations of screen/tmux sessions, both for TTY and non-TTY terminals.


______


## Edit `~/.profile`
[heading__edit_profile]: #edit-profile


**`~/.profile` (snip)**


```bash
##
# Customization for tty with fbterm
# See: https://bbs.archlinux.org/viewtopic.php?id=150473
# See: https://gist.github.com/zellio/5809852
# See: man ucimf
if [[ "$(tty)" == '/dev/tty6' ]] && [[ -e "$(which fbterm)" ]]; then
  export LC_ALL=en_US.UTF-8
  FBTERM=1 exec fbterm --font-size=20 -i fbterm_ucimf
fi
```


> Note, the `'/dev/tty6'` path may need adjustment depending upon preexisting host configurations. The above configurations target one specific TTY session, this is to prevent issues that may be caused by having `fbterm` on the same session as those that launch window managers.


______


## Usage
[heading__usage]: #usage


On many hosts the function keys, combined with <kbd>Ctrl</kbd> (or <kbd>Cmd</kbd>) and <kbd>Alt</kbd> keys, may be used to change to a given TTY session.

For example to switch to TTY6 would be <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>F6</kbd>, which is the session configured previously for `fbterm`. And to switch to TTY7 would be <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>F7</kbd>, which is often the session configured for window managers.


Switching to a TTY session without a window manager will present a login prompt, eg...


>     Linux Mint 19.2 Tina TTY 6
>     hostname login:


... after login, attempt to send some ANSI color escape sequences...


```bash
printf '\033[38;2;255;0;0m%s\033[00m\n' "Red Foreground"

printf '\033[38;2;0;255;0m%s\033[00m\n' "Green Foreground"

printf '\033[38;2;0;0;255m%s\033[00m\n' "Blue Foreground"
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

