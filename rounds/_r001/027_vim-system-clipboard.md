---
layout: post
title: Vim System Clipboard
date: 2021-01-31 19:02:38 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to enable Linux clipboard support in Vim
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1356082605200990213
  title: Link to Tweet for this post

attribution:
  links:
    - text: Accessing the system clipboard
      href: https://vim.fandom.com/wiki/Accessing_the_system_clipboard
      title: Tips and tricks for accessing clipboard within Vim
      class: fa fa-wikipedia-w
---



Recently I configured Vim to utilize the system clipboard as the default _buffer_ to yank to and put from, this post covers the relevant details on how I enabled such functionality.


---


- [Check Clipboard Support][heading__check_clipboard_support]

- [Install Compatible Version (`apt-get`)][heading__install_compatible_version_aptget]

- [Configure Vim Clipboard][heading__configure_vim_clipboard]

- [Contact and/or Contribute][heading__contact_andor_contribute]

- [Attribution](#heading__attribution)


---



## Check Clipboard Support
[heading__check_clipboard_support]: #check-clipboard-support "Quick command to check if Vim is compiled with clipboard support"


To access the clipboard within Vim `clipboard` support is required within the compiler options, to check run the following command...


```bash
vim --version | grep 'clipboard'
```


Example output...


```
+clipboard         +jumplist          +popupwin          +user_commands
+ex_extra          -mouse_jsbterm     -sun_workshop      +xterm_clipboard
```


... note how both `+cliboard` and `+xterm_clipboard` are prefixed with a plus-sign (`+`), which denotes that Vim was compiled with those options.


______


## Install Compatible Version (`apt-get`)
[heading__install_compatible_version_aptget]: #install-compatible-version-apt-get "Apt command that _should_ install Vim with clipboard support pre-compiled"


Debian based distributions may utilize `vim-gnome` to install a version of Vim that is pre-compiled with clipboard support, eg...


```bash
sudo apt-get install vim-gnome
```

______


## Configure Vim Clipboard
[heading__configure_vim_clipboard]: #configure-vim-clipboard "Vim configurations that _should_ enable clipboard support"


Once a compatible version of Vim is installed adding the following to the `~/.vimrc` file _should_ enable clipboard support...


```vim
set clipboard=unnamedplus
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

