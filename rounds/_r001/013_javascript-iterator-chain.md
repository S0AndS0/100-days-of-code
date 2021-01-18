---
layout: post
title: JavaScript Iterator Chain
date: 2021-01-17 20:44:22 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of how to chain callback functions with an Iterator/Generator
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1351040607226122241
  title: Link to Tweet for this post

attribution:
  links:
    - text: Dev IO -- Iterators in TypeScript
      href: https://dev.to/gsarciotto/iterators-in-typescript-1d78
      title: Iterators in TypeScript

    - text: Medium -- How to chain functions in JavaScript
      href: https://medium.com/@jamischarles/how-to-chain-functions-in-javascript-6644d44793fd
      title: How to chain functions in JavaScript

    - text: 'Web Masters -- How do I open the JavaScript console in different browsers?'
      href: https://webmasters.stackexchange.com/questions/8525/
      title: How do I open the JavaScript console in different browsers?
      class: fa fa-stack-exchange
---


> Example of how to chain callback functions with an Iterator/Generator


---


- [Generator/Iterator Overview][heading__generatoriterator_overview]

  - [Generator From Array Example][heading__generator_from_array_example]
  - [Generator From String Example][heading__generator_from_string_example]
  - [Generator From Object Example][heading__generator_from_object_example]

- [Iterator Chain Source Code][heading__iterator_chain_source_code]

  - [Iterator Chain Overview][heading__iterator_chain_overview]
  - [Iterator Chain Usage Example][heading__iterator_chain_usage_example]

- [Explore With Browser Console][heading__explore_with_browser_console]

- [Contact and/or Contribute][heading__contact_andor_contribute]

- [Attribution](heading__attribution)


---


## Generator/Iterator Overview
[heading__generatoriterator_overview]: #generatoriterator-overview


Quick crash-course for JavaScript generators so that all readers have some foundations for the syntax.


An iterator/generator has a `next()` method that returns an object with `value` and `done` keys; `value` maybe of any type, and `done` should be Boolean which tells caller(s) if iteration is finished. The `value` may be computed at the time of calling `next()`, which is useful for consuming buffers or other data sources of unknown, or infinite, length.


---


### Generator From Array Example
[heading__generator_from_array_example]: #generator-from-array-example

Generators may be built by functions that `yield` using the following syntax...


```javascript
function* generatorFromArray(array) {
  for (let value of array) {
    yield value;
  }
}


const list_iter = generatorFromArray([1, 2, 3]);


console.log(list_iter.next());
//> { value: 1, done: false }
console.log(list_iter.next());
//> { value: 2, done: false }
console.log(list_iter.next());
//> { value: 3, done: false }
console.log(list_iter.next());
//> { value: undefined, done: true }
```


---


### Generator From String Example
[heading__generator_from_string_example]: #generator-from-string-example


The _`for (let value of iter)`_ syntax implicitly calls the `next()` method, passing/assigning `value` variable, until `done` reports `true`. When a generator returns `done` of `true` then `for` loops automatically `break`...


```javascript
function* generatorFromString(str) {
  for (let character of [...str]) {
    yield character;
  }
}


const str_iter = generatorFromString('Spam Flavor');
for (let c of str_iter) {
  console.log(c);
}
//> 'S'
//> 'p'
//> 'a'
//> 'm'
//> ' '
//> 'F'
//> 'l'
//> 'a'
//> 'v'
//> 'o'
//> 'r'
```


---


### Generator From Object Example
[heading__generator_from_object_example]: #generator-from-object-example

Here's a `while` loop example...


```javascript
function* generatorFromObject(data) {
  for (let key in data) {
    yield data[key];
  }
}


const iter = generatorFromObject({one: 1, two: 2, three: 3});
let iter_result = iter.next();
while(!iter_result.done) {
  console.log(iter_result.value);
  iter_result = iter.next();
}
//> 1
//> 2
//> 3
```


______


## Iterator Chain Source Code
[heading__iterator_chain_source_code]: #iterator-chain-source-code


The goal is to have a wrapper object that takes an Iterator/Generator, and each `next()` is called executes a sequence of callback functions. So far the following is a preview of a project that I'll be publishing in the future...


```javascript
'use strict';


/**
 * Wrapper for Iterator/Generators that chains an array of callbacks
 * @author S0AndS0
 * @license AGPL-3.0
 */
class Iterator_Chain {
  constructor(iterator) {
    this.iterator = iterator;
    this.callbacks = [];
    this.value = undefined;
    this.done = false;
  }

  next() {
    const yielded_result = this.iterator.next();
    if (yielded_result.done) {
      this.done = yielded_result.done;
      this.value = yielded_result.value;
    } else {
      const { value, done } = this.callbacks.reduce((accumulator, callback) => {
        return {
          value: callback(accumulator.value, this),
          done: accumulator.done,
        };
      }, yielded_result);

      this.value = value;
      this.done = done;
    }

    return this;
  }

  [Symbol.iterator]() {
    return this;
  }
}


if (typeof module !== 'undefined') {
  module.exports = Iterator_Chain;
}
```

<script>
'use strict';


/**
 * Wrapper for Iterator/Generators that chains an array of callbacks
 * @author S0AndS0
 * @license AGPL-3.0
 * @example
 * function* generatorFromArray(array) {
 *   for (let value of array) {
 *     yield value;
 *   }
 * }
 *
 * const ic = new Iterator_Chain(generatorFromArray([9, 8, 7]));
 * ic.callbacks.push((value) => { return value + 1; });
 * ic.callbacks.push((value) => { return value * 2; });
 * ic.callbacks.push((value) => { return value / 3; });
 *
 * for (let value of ic) {
 *   console.log(value);
 * }
 * //> 6.666666666666667
 * //> 6
 * //> 5.333333333333333
 */
class Iterator_Chain {
  constructor(iterator) {
    this.iterator = iterator;
    this.callbacks = [];
    this.value = undefined;
    this.done = false;
  }

  next() {
    const yielded_result = this.iterator.next();
    if (yielded_result.done) {
      this.done = yielded_result.done;
      this.value = yielded_result.value;
    } else {
      const { value, done } = this.callbacks.reduce((accumulator, callback) => {
        return {
          value: callback(accumulator.value, this),
          done: accumulator.done,
        };
      }, yielded_result);

      this.value = value;
      this.done = done;
    }

    return this;
  }

  [Symbol.iterator]() {
    return this;
  }
}


if (typeof module !== 'undefined') {
  module.exports = Iterator_Chain;
}
</script>


---


### Iterator Chain Overview
[heading__iterator_chain_overview]: #iterator-chain-overview


Because the `Iterator_Chain` class has `done` and `value` properties, it may return itself as a yielded result. And because the `Iterator_Chain` class has a `next()` method, it may be called by `for` loops.


---


### Iterator Chain Usage Example
[heading__iterator_chain_usage_example]: #iterator-chain-usage-example


Here's an example of chaining three callbacks that execute for each value from an iterator...


```javascript
function* generatorFromArray(array) {
  for (let value of array) {
    yield value;
  }
}


const chained_iterator = new Iterator_Chain(generatorFromArray([9, 8, 7, 6, 5]));

chained_iterator.callbacks.push((value) => { return value + 1; });
chained_iterator.callbacks.push((value) => { return value * 2; });
chained_iterator.callbacks.push((value) => { return value / 3; });


let count = 0;
while (count < 3) {
  console.log(chained_iterator.next().value);
  count++;
}
//> 6.666666666666667
//> 6
//> 5.333333333333333
```


... Note, one of the other benefits of Generator/Iterator objects is that execution may be halted midway through.


______


## Explore With Browser Console
[heading__explore_with_browser_console]: #explore-with-browser-console


This page includes within it's source a copy of the above `class`, so readers that are utilizing a compatible web-browser may open the JavaScript console and experiment. Here's a quick list of browsers and the keyboard shortcuts that'll open the console...


- Chrome -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>K</kbd>

- Firefox -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>J</kbd>

- Opera -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd>

- Safari -- <kbd>Cmd</kbd> + <kbd>Opt</kbd> + <kbd>c</kbd>


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

