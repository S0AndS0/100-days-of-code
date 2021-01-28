---
layout: post
title: TypeScript InstanceType Madness
date: 2021-01-26 20:45:31 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to utilize `InstanceType` within nested `static` method
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1354294136267005953
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- Access to static properties via this.constructor in typescript
      href: https://stackoverflow.com/questions/33387318/
      title: Access to static properties via this.constructor in typescript
      class: fa fa-stack-overflow

    - text: 'StackOverflow -- Typescript: Pass generic class to function parameter'
      href: https://stackoverflow.com/questions/49740540/
      title: 'Typescript: Pass generic class to function parameter'
      class: fa fa-stack-overflow
---



Today I had to figure out how to utilize `InstanceType` within nested `static` method for a project that I recently published. What follows are simplified TypeScript examples...


```typescript
'use strict';


class Testy {
  static is_this_that(that: any): boolean {
    const checker = function(instance: InstanceType<Testy>): boolean {
      return that instanceof instance;
    }

    return checker(this);
  }
}


interface Testy {
  new(...args: any[]): Testy;
}


console.log('Testy.is_this_that(new Testy()) ->', Testy.is_this_that(new Testy()));

console.log('Testy.is_this_that(new Array()) ->', Testy.is_this_that(new Array()));
```


Expect output similar to...


```
Testy.is_this_that(new Testy()) -> true
Testy.is_this_that(new Array()) -> false
```


Without `new(...args: any[]): Testy` within an `interface` definition the following error would be reported...


```
ts/testy.ts|5 col 53 error|
  Type 'Testy' does not satisfy the constraint 'new (...args: any) => any'.
  Type 'Testy' provides no match for the signature 'new (...args: any): any'.
```


---


Things get a bit more complicated when writing a class that has instance methods accessing `static` methods, eg...


```TypeScript
'use strict';


class Testy {
  static is_this_that(that: any): boolean {
    const checker = function(instance: InstanceType<Testy>): boolean {
      return that instanceof instance;
    }

    return checker(this);
  }

  is_this_testy(): boolean {
    return this.constructor.is_that_this(this);
  }
}


interface Testy {
  new(...args: any[]): Testy;
}


console.log('Testy.is_this_that(new Testy()) ->', Testy.is_this_that(new Testy()));

console.log('Testy.is_this_that(new Array()) ->', Testy.is_this_that(new Array()));
```


**Example errors**


```
ts/scratch-pad.ts|9 col 20 error|
  Argument of type 'typeof Testy' is not assignable to parameter of type 'Testy'.
  Property 'is_this_that' is missing in type 'typeof Testy' but required in type 'Testy'.

ts/scratch-pad.ts|13 col 29 error|
  Property 'is_that_this' does not exist on type 'Function'.
```


For the second TypeScript error above, there be a possible fix demonstrated within post [001 014 TypeScript Static Methods][link__100_days_of_code__r001_014_typescript_static_methods], however, for the first of above listed errors the best option I could find was replacing _`InstanceType<Testy>`_ with _`InstanceType<any>`_... which while not ideal does function well enough.


Put together here be the code that I found would transpile without errors...


```typescript
'use strict';


class Testy {
  static is_that_this(that: any) {
    const checker = function(instance: InstanceType<any>) {
      return that instanceof instance;
    }

    return checker(this);
  }

  is_this_that(): boolean {
    return this.constructor.is_that_this(this);
  }
}


interface Testy {
  new(...args: any[]): Testy;
  constructor: typeof Testy;
}


console.log('Testy.is_that_this(new Testy()) ->', Testy.is_that_this(new Testy()));
console.log('Testy.is_that_this(new Array()) ->', Testy.is_that_this(new Array()));
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__100_days_of_code__r001_014_typescript_static_methods]: {{ 'r001/014-typescript-static-methods/' | absolute_url }}

