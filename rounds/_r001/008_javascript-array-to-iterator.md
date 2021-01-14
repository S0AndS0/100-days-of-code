---
layout: post
title: JavaScript Array to Iterator
date: 2021-01-12 16:48:03 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick example function for converting an Array to itarable
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1349182987674521602
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How to document a function returned by a function using JSDoc
      href: https://stackoverflow.com/questions/30012043/
      title: How to document a function returned by a function using JSDoc
      class: fa fa-stack-overflow

    - text: JSDoc -- Yields
      href: https://jsdoc.app/tags-yields.html
      title: How to define value yielded from Generator or Iterator

    - text: JSDoc -- Function
      href: https://jsdoc.app/tags-function.html
      title: How to mark an object as a function
---



Quick example function for converting an Array to itarable...


```javascript
/**
 * Yields elements from Array one at a time
 * @param {any[]} list - Array of elements to convert to itarable
 * @returns {Generator_From_Array}
 */
function arrayToIterator(list) {
  /**
   * @function Generator_From_Array
   * @yields {any}
   */
  const generator = function* () {
    for (let item of list) {
      yield item;
    }
  };

  return generator();
}
```


Iterators/Generators are generally a memory efficient way of handling data, especially when parsing through large sets. Following is a simple example of how to _walk_ through two iterators built from arrays using the `arrayToIterator` function...


```javascript
const iter_one = arrayToIterator([1, 2, 3]);
const iter_two = arrayToIterator([9, 8, 7]);

let iter_one_next = iter_one.next();
let iter_two_next = iter_two.next();
do {
  console.log(`one / two -> ${iter_one_next.value} / ${iter_two_next.value}`);

  iter_one_next = iter_one.next();
  iter_two_next = iter_two.next();
} while(!iter_one_next.done && !iter_two_next.done)
```


Expect console output similar to...


```
one / two -> 1 / 9
one / two -> 2 / 8
one / two -> 3 / 7
```


---


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


---


[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

