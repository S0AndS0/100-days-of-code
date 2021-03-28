---
layout: post
title: Vim Edit Macro
date: 2021-03-27 21:01:07 -0700
#date_updated:  # Optional and formatted like 'date' above
description: How to write, read, and edit Vim macros
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1376027409926004739
  title: Link to Tweet for this post
---



Today I invested some time into converting HTML `picture` elements to YAML (FrontMatter) configurations for the [`install-linux-guides/usb-uefi-compatible`][link__install_linux_guides__usb_uefi_commpatible] guide, in doing so much was learned about Vim macros so this post will be a bit of a synopsis.


---


- [Example Snips][heading__example_snips]

- [Interacting With Macro Registers][heading__interacting_with_macro_registers]

- [Example Macro][heading__example_macro]

- [Contact and/or Contribute][heading__contact_andor_contribute]


---


______



## Example Snips
[heading__example_snips]: #example-snips


**HTML (snip)**


```html
<picture>
  <source type="image/avif"
          scrset="{{ 'assets/print-screen/first-boot/drivers/menu-driver-manager/menu-driver-manager.avif' | absolute_url }}" />
  <source type="image/jpeg"
          scrset="{{ 'assets/print-screen/first-boot/drivers/menu-driver-manager/menu-driver-manager.jpeg' | absolute_url }}" />
  <source type="image/png"
          scrset="{{ 'assets/print-screen/first-boot/drivers/menu-driver-manager/menu-driver-manager.png' | absolute_url }}" />
  <source type="image/webp"
          scrset="{{ 'assets/print-screen/first-boot/drivers/menu-driver-manager/menu-driver-manager.webp' | absolute_url }}" />
  <img alt="Print screen image of Virtual Machine menu Driver Manager"
       loading="lazy"
       decoding="async"
       width="800"
       height="600"
       src="{{ 'assets/print-screen/first-boot/drivers/menu-driver-manager/menu-driver-manager.jpeg' | absolute_url }}" />
</picture>
```


**YAML (snip)**


```yaml
pictures:
  menu-driver-manager:
    url:
      base: assets/print-screen/first-boot/drivers/menu-driver-manager/
      filter: relative_url

    img:
      alt: Print screen image of Virtual Machine menu Driver Manager
      src: menu-driver-manager.jpeg
      width: 800
      height: 600
      loading: lazy
      decoding: async

    sources:
      - scrset: menu-driver-manager.avif
      - scrset: menu-driver-manager.jpeg
      - scrset: menu-driver-manager.png
      - scrset: menu-driver-manager.webp
```


... I had multiple files to preform these conversions, thankfully Vim has features to record macros; which are a method of saving and replaying keystrokes.


So all I had to do was record converting one `picture` element to YAML configuration block to a macro, then replay it _n_ amount of times for all files that needed converted.


______


## Interacting With Macro Registers
[heading__interacting_with_macro_registers]: #interacting-with-macro-registers


To begin recording a macor in Vim within Normal mode press the <kbd>q</kbd> key then another letter, eg. <kbd>q</kbd> <kbd>w</kdb> will record key strokes the _`w`_ register.


To finish recording press the <kbd>q</kbd> again within Normal mode.


Because the keystrokes are saved to a register the content may be pasted (put) for inspection, eg...


<kbd>"</kbd> <kbd>w</kbd> <kbd>p</kbd>


... will _put_ keystrokes from _`w`_ into the current buffer/line


This is useful for inspecting, and optionally correcting mistakes, within a macro. And may be useful for saving, or backing-up, macros for reuse.


______



## Example Macro
[heading__example_macro]: #example-macro


Suppose for example that the following HTML needs an _`a`_ tag to wrap the _`link`_ word...


```html
<p>
  Some text with an embeded link to somewhere
</p>
```


... eg. above transmuted into below...


```html
<p>
  Some text with an embeded <a href="#">link</a> to somewhere
</p>
```


For a _one-off_ that's relatively easy to do, however, for doing such edits en-masse a macro can save much time and keystrokes.


Following are the sequences of keystrokes that where recorded...


```
/p>^M/link^Mciw<a></a>^[<80><fd>aF>pF>i href="#"^[
```


**Explanation**


- `/p>` search for _`p>`_
- `^M` escape-code for <kbd>Enter</kdb>

- `/link` search for _`link`_
- `^M` escape-code for <kbd>Enter</kdb>
  - `ciw` change in word, cuts current word into default register and starts Insert mode
    - `<a></a>` insert literal string of characters

- `^[<80><fd>a` escape-code for <kbd>Esc</kbd> key
  - `F>` backwards search current line for _`>`_
    - `p` put content of default paste register _(`link`)_ after cursor position

  - `F>` backwards search current line for _`>`_
    - `i` start Insert mode
      - ` href="#"` insert literal string of characters
      - `^[` also an escape-code for <kbd>Esc</kbd> key


... to make the above macro re-usable/generic, and the default for _`@a`_ within HTML files, the above may be translated into below configurations...


**`~/.vimrc` (snip)**


```vim
if &filetype == 'html'
  let @a = "ciw<a></a>\<ESC>F>pF>i href=\"#\"\<ESC>"
endif
```


> Note, double-quotes _(`"`)_ must be used for _`<ESC>`_, and other key-words, to be expanded; which also means to insert a literal double-quote requires escaping with a back-slash _(`\`)_


Macros are very powerful for saving editing time, and because they can be re-used/saved macros can save time that would otherwise be spent on writing a script or plugin too. In fact many of the plugins that I write where born from a macro that over time required more features, or where useful enough to warrant sharing with others in a more legible format.


______



## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__install_linux_guides__usb_uefi_commpatible]: https://github.com/install-linux-guides/usb-uefi-compatible

