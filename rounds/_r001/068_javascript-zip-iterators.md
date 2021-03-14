---
layout: post
title: JavaScript Zip Iterators
date: 2021-03-13 17:24:30 -0800
#date_updated:  # Optional and formatted like 'date' above
description: JavaScript generator function that zips list of iterables
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



JavaScript generator function that zips arbitrary number iterables...


```javascript
/**
 * Zips values from multiple iterator/generator objects
 * @param {Iterator<any>[]} iterables
 * @yields {any[]}
 */
function* zipIterables(...iterables) {
  while (true) {
    const stats = [];
    const results = [];

    for (const iterable of iterables) {
      const result = iterable.next();
      stats.push(result.done);
      results.push(result.value);
    }

    if (stats.every((stat) => stat === true)) {
      break;
    }

    yield results;
  }
}
```


Few generator and iterator example functions...


```javascript
/**
 * Converts string to character-by-character generator
 */
function* generatorFromString(str) {
  for (let character of [...str]) {
    yield character;
  }
}


/**
 * Converts array to element-by-element generator
 */
function* generatorFromArray(array) {
  for (let value of array) {
    yield value;
  }
}


/**
 * Iterator class that counts by specified amount
 */
class Counter {
  constructor({start = 0, step = 1, stop = Infinity}) {
    this.value = start;
    this.done = false;
    this.step = (step > 0 || step < 0) ? step : 1;

    this.stop = stop;
    if (isNaN(stop)) {
      this.stop = step > 0 ? Infinity : -Infinity;
    }
  }

  next() {
    if (this.stop === this.value) {
      this.done = true;
    }

    if (this.done) {
      this.value = undefined;
      return this;
    }

    this.value += this.step;
    return this;
  }

  [Symbol.iterator]() { return this; }
}
```


Example of initializing each function and class...


```javascript
const counter = new Counter({stop: 18});

const iterate_string = generatorFromString('Spam flavored ham');

const iterate_array = generatorFromArray([
  'I',
  'II',
  'III',
  'IV',
  'V',
  'VI',
  'VII',
  'VIII',
  'IX',
  'X',
]);
```


Example usage and output...


```javascript
const zipper = zipIterables(counter, iterate_string, iterate_array);


for (let values of zipper) {
  console.log({values});
}
//> { values: [ 1, 'S', 'I' ] }
//> { values: [ 2, 'p', 'II' ] }
//> { values: [ 3, 'a', 'III' ] }
//> { values: [ 4, 'm', 'IV' ] }
//> { values: [ 5, ' ', 'V' ] }
//> { values: [ 6, 'f', 'VI' ] }
//> { values: [ 7, 'l', 'VII' ] }
//> { values: [ 8, 'a', 'VIII' ] }
//> { values: [ 9, 'v', 'IX' ] }
//> { values: [ 10, 'o', 'X' ] }
//> { values: [ 11, 'r', undefined ] }
//> { values: [ 12, 'e', undefined ] }
//> { values: [ 13, 'd', undefined ] }
//> { values: [ 14, ' ', undefined ] }
//> { values: [ 15, 'h', undefined ] }
//> { values: [ 16, 'a', undefined ] }
//> { values: [ 17, 'm', undefined ] }
//> { values: [ 18, undefined, undefined ] }
```


**Warning** `zipper` may get _stuck_ if any iterables fail to provide `{ done: true }` result status


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

