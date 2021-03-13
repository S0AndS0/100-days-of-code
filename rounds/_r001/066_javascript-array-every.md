---
layout: post
title: JavaScript Array Every
date: 2021-03-11 15:36:10 -0800
#date_updated:  # Optional and formatted like 'date' above
description: More tricks for writing succinct JavaScript checks
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1370158706214772736
  title: Link to Tweet for this post

attribution:
  links:
    - text: MDN -- `Array.prototype.every()`
      href: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every
      title: '`Array.prototype.every()`'
      class: fa fa-firefox
---



Similar to the [post of yesterday][link__100_days_of_code__r001_065__javascript_array_includes] regarding logical OR chaining, it is possible to replace logical AND chaining with a JavaScript array method; namely the `Array.every` method.


For example consider the following function that returns `true` for unsigned positive integers, and `false` otherwise...


```javascript
function fn1(arg) {
  if (!isNaN(arg) && arg > 0 && Number.parseInt(arg) == arg) {
    return true;
  }
  return false;
}


console.log(fn1('spam'));
//> false
console.log(fn1(NaN));
//> false
console.log(fn1(4.2));
//> false
console.log(fn1(-3));
//> false
console.log((fn1(99)));
//> true
```


Leveraging `Array.every` and rewriting conditions as a list of callbacks, above may be expressed as...


```javascript
function fn2(arg) {
  return [
    n => !isNaN(n),
    n => n > 0,
    n => Number.parseInt(n) == n,
  ].every(callback => callback(arg));
}
```


While not necessarily simpler to write initially, personally I find _`fn2`_ to be less prone to having errors introduced by future edits, and much easier to read when three or more checks must be chained.


---


Side note, the `Array.every` method may occasionally replace traditional _`for`_ loops that include _`break`_ conditions, eg...


```javascript
function fn3(list, accumulator = []) {
  for (const value of list) {
    if (value == 'stop') {
      break
    }
    accumulator.push(value);
  }

  return accumulator;
}
```


... Above _`fn3`_ is mostly equivalent to _`fn4`_ bellow...


```javascript
function fn4(list, accumulator = []) {
  list.every((value) => {
    if (value != 'stop') {
      accumulator.push(value);
      return true;
    }
  });

  return accumulator;
}
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__100_days_of_code__r001_065__javascript_array_includes]: {{ 'r001/065-javascript-array-includes/' | absolute_url }} "Post -- JavaScript Array Includes"

