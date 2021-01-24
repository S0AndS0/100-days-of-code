---
layout: post
title: JavaScript Iterator Class
date: 2021-01-22 22:22:12 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of self-modifying Iterator class
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1352865693033754631
  title: Link to Tweet for this post
---



Invested in documentation and testing of a new JavaScript project that I've been writing, should be ready and published tomorrow. Until then here's a quick Iterator class example...


```javascript
/**
 * @pram {number} value - Starting number for counting
 */
class Counter {
  constructor(value = 0) {
    this.value = isNaN(value)? 0: value;
    this.done = false;
  }

  next() {
    this.value++;
    return this;
  }

  [Symbol.iterator]() {
    return this;
  }
};
```


And some example usage...


```javascript
const counter = new Counter();

for (let count of counter) {
  if (count > 9) {
    break;
  }
  console.log('count ->', count);
}
```


Iterators are super useful for parsing and/or computing data that may be of undetermined, or infinite, length.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

