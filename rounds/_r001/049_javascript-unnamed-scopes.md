---
layout: post
title: JavaScript Unnamed Scopes
date: 2021-02-22 15:25:04 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Use cases for unnamed scopes in JavaScript console and files
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1363994319540125702
  title: Link to Tweet for this post
---



When testing ideas within a console, unnamed scopes can be useful...


```javascript
{
  const x = 42;
  console.log({x});
  //> { x: 42 }
}


{
  const x = 'forty-two';
  console.log({x});
  //> { x: "forty-two" }
}
```


... because of the curly-braces the two `x` assignments do not conflict with one-another.


The same trick may be used within script, or module, files to avoid certain issues with transpilers too...


**`index.js`**


```javascript
#!/usr/bin/env node


'use strict'


const log_path = 'some-where/file.log'


/**
 * File system only commands...
 */
{
  const fs = require('fs');

  const log_dir = log_path.split('/').slice(0, -1).join('/');

  try {
    fs.readdirSync(log_dir);
  } catch (error) {
    if (error.message === `ENOENT: no such file or directory, scandir '${log_dir}'`) {
      fs.mkdirSync('some-path');
    } else {
      throw error;
    }
  }
}


/**
 * ... Non file system commands
 */
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

