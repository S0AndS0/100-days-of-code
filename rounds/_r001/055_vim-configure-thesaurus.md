---
layout: post
title: Vim Configure Thesaurus
date: 2021-02-28 15:22:21 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Guide for adding, and using, thesaurus file(s) with Vim
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1366172309783015425
  title: Link to Tweet for this post

attribution:
  links:
    - text: Ask Ubuntu -- Remove First n Lines of a Large Text File
      href: https://askubuntu.com/questions/410196/
      title: Remove First n Lines of a Large Text File
      class: fa fa-stack-exchange

    - text: Unix StackExchange -- Extract only a specific file from a zipped archive to a given directory
      href: https://unix.stackexchange.com/questions/14120/
      title: Extract only a specific file from a zipped archive to a given directory
      class: fa fa-stack-exchange

    - text: Vim Issue `629` -- Broken link on :h thesaurus
      href: https://github.com/vim/vim/issues/629#issuecomment-443293282
      title: Broken link on :h thesaurus
---



While reading through various Vim help pages, as one does from time-to-time, I ran across `:help thesaurus` which has some hints on using a thesaurus file. But didn't have a fully functional step-by-step guide on obtaining the required thesaurus file. This guide will cover how to obtain an English thesaurus for Vim as well as review configurations and usage.


---


- [Download][heading__download]

- [Unzip][heading__unzip]

- [Configure][heading__configure]

- [Usage][heading__usage]

- [Contact and/or Contribute][heading__contact_andor_contribute]

- [Attribution](#heading__attribution)


---


## Download
[heading__download]: #download


Make a directory for thesaurus files...


```bash
mkdir -vp ~/.vim/thesaurus
```


Download Zip archive from GitHub...


```bash
torrific-curl -o /tmp/thesaurus_pkg.zip\
              -L https://github.com/vim/vim/files/2634525/thesaurus_pkg.zip
```


______


## Unzip
[heading__unzip]: #unzip


Unzip `thesaurus_pkg/thesaurus.txt` file to `~/.vim/thesaurus/english.txt` path...


```bash
unzip -p /tmp/thesaurus_pkg.zip thesaurus_pkg/thesaurus.txt\
      | tail -n +3\
      | tee ~/.vim/thesaurus/english.txt 1>/dev/null
```


Unzip `thesaurus_pkg/license.readme` file to `~/.vim/thesaurus/english-license.txt`


```bash
unzip -p /tmp/thesaurus_pkg.zip thesaurus_pkg/license.readme\
      | tee ~/.vim/thesaurus/english-license.txt 1>/dev/null
```


______


## Configure
[heading__configure]: #configure


Append thesaurus setting to `~/.vimrc` configurations...


```bash
tee -a ~/.vimrc 1>/dev/null <<'EOF'
set thesaurus+=$HOME/.vim/thesaurus/english.txt
EOF
```


______


## Usage
[heading__usage]: #usage


When cursor is on or just after a word, and while in Insert mode


- <kbd>Ctrl</kbd>^<kbd>x</kbd> <kbd>Ctrl</kbd>^<kbd>t</kbd> keyboard shortcut will open a menu with similar words

- <kbd>Ctrl</kbd>^<kbd>e</kbd> will close the menu without changing to selected word

- <kbd>Ctrl</kbd>^<kbd>n</kbd> selects the next word in menu

- <kbd>Ctrl</kbd>^<kbd>p</kbd> selects the previously word in menu

- Inputting almost any other key will replace word in buffer with word selected in menu


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

