---
layout: post
title: TypeScript Getters and Setters
date: 2021-01-24 20:41:47 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Type-hints for Object that has `__lookupGetter__` and `__lookupSetter__` methods
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1353565016071565312
  title: Link to Tweet for this post
---



> Type-hints for Object that has `__lookupGetter__` and `__lookupSetter__` methods


---


- [Example `interface` Fix][heading__example_interface_fix]

- [Fully Functioning Example][heading__fully_functioning_example]
  - [Example Usage][heading__example_usage]
  - [TypeScript Configurations][heading__typescript_configurations]

- [Contact and/or Contribute][heading__contact_andor_contribute]


---


Recently I ran into issues using `__lookupGetter__` and `__lookupSetter__` methods in TypeScript to check if `get` and/or `set` method(s) of a given name where present on a class Object. TypeScript was throwing errors similar to...


```
Property '__lookupGetter__' does not exist on type 'NameOfClass'
```


... and...


```
Property '__lookupSetter__' does not exist on type 'NameOfClass'
```


______


## Example `interface` Fix
[heading__example_interface_fix]: #example-interface-fix


Following `interface` is how I hinted to TypeScript that such properties exist...


```typescript
interface NameOfClass {
  __lookupGetter__: (target: string) => Function | undefined;
  __lookupSetter__: (target: string) => Function | undefined;
}
```


---


## Fully Functioning Example
[heading__fully_functioning_example]: #fully-functioning-example


Following `Person` class demonstrates defining custom TypeScript `interface` and `type` for allowing `get`, `set`, and `static` methods to transpile without errors...


**`ts/person.ts`**


```typescript
'use strict';


/**
 * Example class for demonstrating custom get/set methods
 * @author S0AndS0
 * @license AGPL-3.0
 */
class Person {
  private storage: Person_Storage;

  /**
   * Builds new instance of Person
   * @example
   * let bob = new Person('bob', 'smith');
   * console.log(bob.full_name);
   * //> Bob Smith
   */
  constructor(...args: string[]) {
    this.storage = { first_name: '' };

    if (Array.isArray(args)) {
      if (args.length >= 1) {
        this.first_name = args[0];
      } else {
        throw new TypeError();
      }
      if (args.length > 2) {
        this.middle_name = args[1];
        this.last_name = args[2];
      } else if (args.length === 2) {
        this.last_name = args[1];
      }
    } else {
      throw new TypeError('Name arguments are required');
    }
  }

  /**
   * Stores first name as string
   */
  set first_name(value: string) {
    this.storage.first_name = this.constructor.titleCase(value);
  }

  /**
   * Returns stored first name
   * @return {string}
   */
  get first_name(): string {
    return this.storage.first_name.toString();
  }

  /**
   * Stores middle name as string
   */
  set middle_name(value: string) {
    this.storage.middle_name = this.constructor.titleCase(value);
  }

  /**
   * Returns stored middle name if available, or an empty string if not assigned
   * @return {string}
   */
  get middle_name(): string {
    if (this.storage.middle_name !== undefined) {
      return this.storage.middle_name.toString();
    }
    return '';
  }

  /**
   * Stores last name as string
   */
  set last_name(value: string) {
    this.storage.last_name = this.constructor.titleCase(value);
  }

  /**
   * Returns stored last name if available, or an empty string if not assigned
   * @return {string}
   */
  get last_name(): string {
    if (this.storage.last_name !== undefined) {
      return this.storage.last_name.toString();
    }
    return '';
  }

  /**
   * Builds name string from stored parts
   * @return {string}
   */
  get full_name(): string {
    let results = this.first_name;

    if (this.middle_name !== undefined) {
      results = `${results} ${this.middle_name}`;
    }
    if (this.last_name !== undefined) {
      results = `${results} ${this.last_name}`;
    }

    return results;
  }

  static titleCase(value: string): string {
    let results = [...value][0].toUpperCase();
    results = `${results}${[...value].slice(1).join('').toLowerCase()}`
    return results;
  }
}


if (typeof module !== 'undefined') {
  module.exports = { Person };
}


/**
 * ===========================================================================
 *                  Custom TypeScript interfaces and types
 * ===========================================================================
 */
interface Person {
  __lookupGetter__: (target: string) => Function | undefined;
  __lookupSetter__: (target: string) => Function | undefined;
  constructor: typeof Person;
}


type Person_Storage = {
  first_name: string;
  middle_name?: string;
  last_name?: string;
};
```


---


### Example Usage
[heading__example_usage]: #example-usage


Quick example of utilizing `class` from above file...


**`ts/example-usage.ts`**


```javascript
'use strict';


const { Person } = require('./person');


const bob = new Person('Bob', 'Smith');

console.log(bob.__lookupGetter__('full_name'))
//> [Function: get full_name]

console.log(bob.__lookupSetter__('full_name'))
//> undefined
```


---


### TypeScript Configurations
[heading__typescript_configurations]: #typescript-configurations


For completeness here are the TypeScript configurations used for examples on this page...


**`tscofig.json`**


```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "es6",
    "lib": [ "dom", "es2017" ],
    "outDir": "",
    "sourceMap": true,
    "strictNullChecks": true,
    "noImplicitAny": true,
    "moduleResolution": "node"
  },
  "include": [ "ts/**/*" ]
}
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

