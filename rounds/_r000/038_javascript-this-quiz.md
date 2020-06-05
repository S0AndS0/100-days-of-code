---
layout: post
title: JavaScript `this` quiz
date: 2020-06-04 09:48:50 -0700
#date_updated:  # Optional and formatted like Thu Jun  4 09:48:50 PDT 2020 above
description: Quick example of `this` scope and one big gotcha
time_to_live: 1800
---



------


- [Hints][heading__hints]

- [Answers][heading__answers]

- [More Resources][heading__more_resources]


------


No peeking, what's `this.prop` value?...


```javascript
this.prop = 'ham';

function fn(value) {
  this.prop = value;
  return this.prop;
}

var g = new fn('spam');

console.log('1', this.prop);
console.log('2', g.prop);

fn('jam');
console.log('3', this.prop);
```


```
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
```


## Hints
[heading__hints]: #hints


- `1` is calling the global scoped value of `this`

- `2` the `new` keyword, which starts a _new_ execution scope

- `3` is why `class` _syntactic sugar_ is often a good idea for functions that utilize `this`


```
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
```


## Answers
[heading__answers]: #answers


```javascript
//> 1 ham
//> 2 spam
//> 3 jam
```


## More Resources
[heading__more_resources]: #more-resources


- [`this` blog post](https://s0ands0.github.io/javascript/this/) has more examples

- [Mozilla Developer -- `this`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

- [StackOverflow -- How does the “this” keyword work?](https://stackoverflow.com/questions/3127429/how-does-the-this-keyword-work)

- [YouTube -- Fireship -- What is THIS in JavaScript? in 100 seconds](https://www.youtube.com/watch?v=YOlr79NaAtQ)
