---
layout: post
title: Vim JSON to Dictionary
date: 2021-02-06 20:00:01 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to read, and parse, JSON files within Vim script
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1358265058363662337
  title: Link to Tweet for this post
---



Some of the Vim plugins that I maintain allow for configuration via JSON file(s). Here is a quick example on how to read, and parse, JSON files within Vim scripts or plugins...


**`test.json`**


```json
{
  "boolean": true,
  "string": "Spam flavored ham",
  "number": 42
}
```


Example Vim Ex mode commands...


```vim
let b:data = json_decode(join(readfile('./test.json'), ''))

echo b:data['string']
"> Spam flavored ham
```


- `readfile` returns an array/list of lines

- `join` converts an array/list to string

- `json_decode` converts a JSON string into Vim dictionary-like data structure


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

