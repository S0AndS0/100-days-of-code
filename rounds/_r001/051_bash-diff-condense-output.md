---
layout: post
title: Bash Diff Condense Output
date: 2021-02-24 16:17:06 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Useful options to condense `diff` output
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



Useful options to condense `diff` output...


```bash
diff --side-by-side\
     --suppress-blank-empty\
     --suppress-common-lines\
     <file-one> <file-two>
```


- `--side-by-side` option will output in two columns

- `--suppress-blank-empty` option will suppress space or tab before empty output lines

- `--suppress-common-lines` option will prevent outputting common lines


**`file-one.txt` (example)**


```text
ham
flavored
spam
```


**`file-two.txt` (example)**


```text
lamb
flavored
spam
```


Example command...


```bash
diff --side-by-side --suppress-common-lines file-one.txt file-two.txt
#> ham              | lamb
```


______



## Attribution
[heading__attribution]: #attribution


- `man diff`


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"


