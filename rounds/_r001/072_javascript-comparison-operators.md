---
layout: post
title: JavaScript Comparison Operators
date: 2021-03-17 16:48:57 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Peek under the hood of how JavaScript compares various data types
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1372336108734976005
  title: Link to Tweet for this post

attribution:
  links:
    - text: Medium -- Comparing Objects in JavaScript
      href: https://medium.com/javascript-in-plain-english/comparing-objects-in-javascript-ce2dc1f3de7f
      title: Comparing Objects in JavaScript
---



JavaScript has two base data kinds _`Object`_ and _`Primitive`_.


Primitives are imutable and, generally, each map to the same point in memory; for example...


```javascript
const p0 = 4;
const p1 = 4;

console.log(p0 === p1);
//> true
```


... both _`p0`_ and _`p1`_ are equal not because each contain the value _`4`_, but because both point to the same location in memory.


Objects, however are a bit more tricky, eg...


```javascript
const o0 = { value: 4 };
const o1 = { value: 4 };

console.log(o0 === o1);
//> false
```


... both _`o0`_ and _`o1`_ above contain the same data, but are not equal because each point to different locations in memory. Where as _`o2`_ and _`o3`_ below are equal because both point to the same memory location...


```javascript
const o2 = { list: [] };
const o3 = o2;

console.log(o2 === o3);
//> true
```


Under the hood the _`===`_ operator can be thought of impicitly calling the `Object.is` method, eg...


```javascript
Object.is(4, 4);
//> true

Object.is({ value: 4 }, { value: 4 });
//> false

Object.is(o2, o3);
//> true
```


Day to day the subtleties of how JavaScript treats _`Primitive`_ and _`Object`_ data usually isn't of any concern. However, knowing about this behaviour can save time, and stress, in specific circumstances... such as debugging a code-base that made use of `String` objects instead of string primitives...


```javascript
const s0 = new String('spam');
const s1 = 'spam';

console.log(s0 === s1);
//> false
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

