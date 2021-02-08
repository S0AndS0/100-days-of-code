---
layout: post
title: JavaScript `valueOf` Method
date: 2021-02-07 16:55:05 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `valueOf` on a custom JavaScript class
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
    - text: MDN -- `Object.prototype.valueOf()`
      href: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf
      title: Object.prototype.valueOf()
      class: fa fa-firefox
---



One of many things I like about Rust and Python languages is that there are methods for implementing arithmetic operations between objects/data-structures. JavaScript however does **not** have such magical methods, instead objects are converted to primitive types via one of (at last count) three methods.


The following is an example of using `valueOf` on a custom JavaScript class...


```javascript
class smallInt {
  constructor(input) {
    if (isNaN(input)) {
      throw new Error('Not a Number!');
    }

    this.value = input | 0;
  }

  valueOf() {
    return this.value;
  }
}

var four = new smallInt('4');
var two = new smallInt(2);

four * two;
//> 8
```


... When JavaScript runs-across arithmetic operators (`+`, `-`, `*`, `/`, `%`), one of the methods that may be used to convert Objects to the left **and** right of the operator is `.valueOf()`, ie. this method is implicit called. A more explicit example of what is going on _under the hood_ may be...


```javascript
var three = new smallInt(3);
var nine = new smallInt(9);

nine.valueOf() / three.valueOf();
//> 3
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

