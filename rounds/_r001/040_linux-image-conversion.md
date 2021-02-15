---
layout: post
title: Linux Image Conversion
date: 2021-02-13 16:30:32 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Command-line tools for converting image formats
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1360749678929797120
  title: Link to Tweet for this post
---



Today I learned some tools for converting images from the Linux command-line.


Converting `.png` images to `.jpeg` and `.avif` is posible via `imagemagic` package, and is installable from Debian/Ubuntu repositories...


```Bash
sudo apt-get install imagemagic
```


... After which the _`convert`_ command may be used similar to _`mv`_, or similar Unix-like commands, eg...


```Bash
convert input.png output.jpeg

convert input.png output.avif
```


---


Converting `.png` images to `.webp` may be achived with the `cwebp` package...


```Bash
sudo apt-get install cwebp
```


... which requires _`-o`_ to denote an output file, eg...


```Bash
cwebp input.png -o output.webp
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

