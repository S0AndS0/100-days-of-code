---
layout: post
title: JavaScript `Symbol.toPrimitive`
date: 2021-02-25 15:20:12 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Examples of utilizing `Symbol.toPrimitive` method
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
    - text: MDN -- `Symbol.toPrimitive`
      href: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive
      title: '`Symbol.toPrimitive`'
      class: fa fa-firefox
---



In other programming languages that I'm failure with, such as Rust and Python, there are _magic_ methods that are called for arithmetic, debugging, or representing data, eg...


```python
class Data:
  def __init__(self, value):
    self.value = value

  def __add__(self, other):
    return self.value + other.value


a = Data(4)
b = Data(2)
print(a + b)
#> 6
```


Until recently one of the things about JavaScript that would occasionally trip me up was implicit type coercion, because there are no `__add__` or `__sub__` methods that are called when `+` or `-` operators are used. Instead there are `toString` and `valueOf`, and recently `[Symbol.toPrimitive]` that are used to coerce types, eg...


```javascript
class Data {
  constructor(value) {
    this.value = value;
  }

  toString() {
    return `${this.value}`;
  }

  valueOf() {
    return Number(this.value);
  }

  [Symbol.toPrimitive](hint) {
    console.log('hint ->', hint);
    switch (hint) {
      case 'number': {
        return this.valueOf();
      }
      case 'string': {
        return this.toString();
      }
      default: {
        console.warn(`Unrecognized hint -> ${hint}`);
        return this.toString();
      }
    }
  }
}


const a = new Data(4);
const b = new Data(2);
console.log(a + b);
//> hint -> "number"
//> hint -> "number"
//> 6
```


While this provides some solutions for writing custom JavaScript objects that explicitly handle type coercion, the lack of support for extending specific arithmetic operators can be troublesome. Because in Python, and many other programming languages, it's possible to write a `__mul__` method that allows a string-like object to be multiplied by a number, where as in JavaScript _`a * b`_ of mixed types will generally result in `NaN`


At the time of writing the _best_ option I've found for JavaScript is to utilize named methods such as `repeat`, eg...


```javascript
console.log('a'.repeat(5) + 'h!');
//> aaaaah!
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

