---
layout: post
title: JavaScript `toString` Method
date: 2021-02-16 22:06:52 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of defining `toString` method on Objects
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1361921123236069379
  title: Link to Tweet for this post

attribution:
  links:
    - text: MDN -- `Object.prototype.toString()`
      href: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString
      title: '`Object.prototype.toString()`'
      class: fa fa-firefox
---



The `toString` method is called implicitly when using Template Literals in JavaScript, eg...


```javascript
var o = {
  toString: function() { return JSON.stringify(this, null, 2); },
  bool: true,
  str: 'Spam',
  num: 42,
};

console.log(`${o}`);
//> {
//>   \"bool\": true,
//>   \"str\": \"Spam\",
//>   \"num\": 42
//> }
```


Function, and classes (which are _sugary_ functions), which are objects too may also benefit from defining a custom `toString` method...


```javascript
class Stringy {
  constructor(value) {
    this.value = value;
  }

  toString() {
    return `${this.value}`;
  }
}

var foo = new Stringy('Foo');
var num = new Stringy(42);

console.log(`${foo} ${num}`);
//> Foo 42
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

