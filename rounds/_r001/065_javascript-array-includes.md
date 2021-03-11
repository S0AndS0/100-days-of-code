---
layout: post
title: JavaScript Array Includes
date: 2021-03-10 15:45:15 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Tricks for writing succinct JavaScript checks
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1369798050890321922
  title: Link to Tweet for this post

attribution:
  links:
    - text: MDN -- `Array.prototype.includes()`
      href: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes
      title: '`Array.prototype.includes()`'
      class: fa fa-firefox
---



One of the common coding patterns, regardless of language, is checking if some value matches a series of possible values, eg...


```javascript
function fn1(arg) {
  if ('NaN' === arg || isNaN(arg)) {
    return true;
  }
  return false
}


console.log(fn1('spam'));
//> false
console.log(fn1('NaN'));
//> true
```


As of ECMA Script 262 it is now possible to write such comparisons in a more succinct fashion via `Array.includes()` method, eg...


```javascript
function fn2(arg) {
  return ['NaN', NaN].includes(arg);
}


console.log(fn2('ham'));
//> false
console.log(fn2(NaN));
//> true
```


Admittedly in above examples this trick does not save much in the way of characters, or cognitive load. However, for larger _chains_ of logical ORing it is possible to save much in maintenance time, and mitigate bugs caused by missing an ORed condition when editing.


For example consider adding case-insensitive matching to _`fn3`_ or _`fn4`_ functions bellow...


```javascript
function fn3(arg) {
  if ('spam' === arg || 'canned ham' === arg || 'salad' === arg || 'hummus') {
    return true;
  }
  return false;
}


function fn4(arg) {
  return ['spam', 'canned ham', 'salad', 'hummus'].includes(arg);
}
```


... Personally I believe _`fn4`_ be easier to add features and/or maintain, eg...


```javascript
function fn4(arg) {
  return [
    'spam',
    'canned ham',
    'salad',
    'hummus',
  ].includes(`${arg}`.toLowerCase());
}
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

