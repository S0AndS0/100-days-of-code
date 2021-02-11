---
layout: post
title: TypeScript is Not a Number
date: 2021-02-09 20:48:53 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Few gotchas regarding type hints with `isNaN` methods
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1359370006514053120
  title: Link to Tweet for this post
---



While writing JavaScript I occasionally must check if a variable contains a number-like value, however, TypeScript does not take kindly to such activities, eg...


```typescript
isNaN('spam');
```


`//> Argument of type 'string' is not assignable to parameter of type 'number'.`


... At the time of publishing this post, the above error is produced because of the default type hints for `isNaN` function defined by TypeScript...


**Example Type Hint**


```typescript
type isNaN = (number: number) => boolean;
```


---


Initially I was tempted to utilize `Number.isNaN` method instead...


```typescript
Number.isNaN(NaN);
//> true
```


... because the type hints are less restrictive...


**Example Type Hint**


```typescript
interface Number {
  isNaN: (number: unknown) => boolean;
}
```


... However, _`Number.isNaN`_ method and _`isNaN`_ function are intended for very different purposes.


For example, `isNaN('spam')` in JavaScript will report _`true`_; as it should. But _`Number.isNaN('spam')`_ will report **_`false`_**!


This is because of _reasons_ of use cases for each;


- `isNaN` function will attempt to coerce input to a number prior to checking

- `Number.isNaN` method literally checks if input is `NaN`


---


So far I've found two workarounds TypeScript errors reported at the top of this post...


**Coerce to Number**


```typescript
isNaN(Number('spam'));
//> true

isNaN(Number(42));
//> false
```


**Value as Number**


```typescript
isNaN('spam' as unknown as number);
//> true

isNaN('spam' as unknown as number);
//> false
```


... Each option has trade-offs.


Coercing to a number via _`isNaN(Number(input))`_ will survive transpiling with TypeScript, meaning that resulting JavaScript will have unnecessary function call to _`Number`_. Though such explicitness may be desired by authors.


Treating input _`as unknown`_ then _`as number`_ will result in slightly less output JavaScript, because transpiling process of TypeScript will remove such type casting. However, coding things this way assumes future versions of ECMAScript will not modify the behavior of `isNaN` function; which for now mostly seems like a safe enough assumption... mostly.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

