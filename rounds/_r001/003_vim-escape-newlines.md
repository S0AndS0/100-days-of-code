---
layout: post
title: Vim Escape Newlines
date: 2021-01-07 20:23:48 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Minor gotcha regarding how to escape newlines within Vim scripts
time_to_live: 1800

tweet:
  url: https://example.com
---



In most scripting and many programming languages are new-line delimited, to ignore newline characters (`\n`) requires a backslash (`\`) prior to the newline character, for example in Bash...


```bash
program-name --param-one something\
             --param-two 'other thing'\
             --flag-of-truth
```


... if escape-characters where shown, the above would be similar to...


```bash
program-name --param-one something\\n
             --param-two 'other thing'\\n
             --flag-of-truth
```


... Effectively this syntax tells the interpreter, or compiler, to ignore the `\n` character(s).


However, in Vim scripts to escape a newline requires the backslash to prefix the content of following line, for example here's how to assign a Vim dictionary while escaping new-lines...


```vim
let l:dictionary = {
     \   'string': 'Spam flavored ham',
     \   'nested': {
     \     'number': 42,
     \   },
     \   'list': [
     \     'first',
     \     'second',
     \     'third',
     \   ],
     \ }


echo string(l:dictionary)
```


Personally I found this to be more than a bit odd. First because most other languages I write treat blocks of code surrounded by `{}` and `[]` somewhat different, and second because generally backslash(s) pressed the character that is escaped. If readers have insights then please share via an [Issue][link__github__s0ands0__100_days_of_code__issue] on GitHub, or reply on [Twitter][link__twitter__s0_and_s0__round_001__day_001].



[link__github__s0ands0__100_days_of_code__issue]: https://github.com/S0AndS0/100-days-of-code/issues "Direct link to GitHub Issues for source-code repository for this site"

[link__twitter__s0_and_s0__round_001__day_001]: {{ post.tweet.url }} "Link to Tweet about Vim script newline escapement"

