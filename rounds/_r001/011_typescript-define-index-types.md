---
layout: post
title: TypeScript Define Index Types
date: 2021-01-15 17:19:34 -0800
#date_updated:  # Optional and formatted like 'date' above
description: How to dynamically get/call class properties/methods
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



One of the recent frustrations that I ran into while writing TypeScript code is accessing class properties, and methods, dynamically; ie. via `obj['key_name']` syntax. Thankfully telling the transpiler/type-checker that such things are okay was not terribly difficult. Here's a quick example `class`...


```typescript
class Classy_Name {
  [key: string]: any;

  constructor(first?: string | undefined, last?: string | undefined) {
    this.first = first;
    this.last = last;
  }

  fullName() {
    return ['first', 'last'].reduce((accumulator: string[], part) => {
      if (this[part] !== undefined) {
        accumulator.push(this[part]);
      }
      return accumulator;
    }, []).join(' ');
  }
}


let classy_name = new Classy_Name('Jayne', 'Cobb');
console.log(classy_name['fullName']());
//> Jayne Cobb
```


The _magic sauce_ is the `[key: string]: any;` type-definition near the top...


```typescript
class Classy_Name {
  [key: string]: any;

  /* ... */
}
```


Which may be further restricted to only allowing methods to be called, eg...


```typescript
class Classy_Methods {
  [key: string]: Function;

  add(a: number, b: number): number {
    return a + b;
  }
}


let classy_methods = new Classy_Methods();
console.log(classy_methods.add(40, 2));
//> 42

console.log(classy_methods['add'](20, 22));
//> 42
```


---


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

