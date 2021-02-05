---
layout: post
title: TypeScript Static Type Hints
date: 2021-02-03 21:57:08 -0800
#date_updated:  # Optional and formatted like 'date' above
description: An experimental way of adding static method, and property, type hints
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1357212779732738050
  title: Link to Tweet for this post

attribution:
  links:
    - text: 'GitHub -- `microsoft/TypeScript` issue `14600` -- Suggestion: Add abstract static methods in classes and static methods in interfaces'
      href: https://github.com/microsoft/TypeScript/issues/14600#issuecomment-488817980
      title: 'Suggestion: Add abstract static methods in classes and static methods in interfaces'

    - text: GitHub -- `microsoft/TypeScript` issue `3841` -- T.constructor should be of type T
      href: https://github.com/Microsoft/TypeScript/issues/3841
      title: T.constructor should be of type T

    - text: TypeScript Language -- Decorators
      href: https://www.typescriptlang.org/docs/handbook/decorators.html
      title: Decorators

    - text: TypeScript Language -- Generics
      href: https://www.typescriptlang.org/docs/handbook/generics.html
      title: Generics
---



I've been fighting with TypeScript for more than a few days with regards to static methods and properties on classes. And how to type hint in such a way that TypeScript produces errors **only** if such structures are misused and/or improperly defined. Digging through GitHub issues showed that others have been struggling in a similar fashion, for years, and _MicroSoft_ has (at least at the time of writing this post) failed to implement a standard way of type hinting static methods and properties.


Frustrating as that all is, the slog through StackOverflow and GitHub Issues was fruitful, because someone by the name of `@theseyi` on GitHub showed a solution. However, beware said solution utilizes experimental features of TypeScript, namely `experimentalDecorators`, which may experience behavioural changes or be removed entirely.


Warnings aside here be the configurations that I tested to be functional with the source code of this post...


**`package.json`**


```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "lib": [ "dom", "es2017" ],
    "outDir": "",
    "sourceMap": true,
    "strictNullChecks": true,
    "noImplicitAny": true,
    "removeComments": true,
    "experimentalDecorators": true,
    "moduleResolution": "node"
  },
  "include": [ "ts/**/*" ]
}
```


... And the source code with commented example lines that _should_ pop transpiler errors where applicable...


**`ts/index.ts`**


```typescript
'use strict';


/**
 * Thanks be to @theseyi of GitHub
 * @see {link} https://github.com/microsoft/TypeScript/issues/14600#issuecomment-488817980
 */
const Static_Contract = <T extends new (...args: unknown[]) => void>():
                        ((c: T) => void) => (_ctor: T): void => {};


/**
 * Define static methods and/or properties
 */
interface Static_Bits<T> {
  new(...args: unknown[]): T;
  static_prop: boolean;
  isMember(instance: any): boolean;
}


/**
 * Define methods and/or properties of instantiated class
 */
interface Instance_Bits {
  instance_prop: string;
}


/**
 * Enable static methods to be called within class methods
 * @see {link} - https://github.com/Microsoft/TypeScript/issues/3841
 */
interface Instance extends Instance_Bits {
  constructor: typeof Instance;
}


/**
 * Decorated to ensure static method/property types are checked
 */
@Static_Contract<Static_Bits<Instance>>()
class Instance {
  constructor(input: string) {
    this.instance_prop = input;
    /* Produce errors about `Instance_Bits`/`Instance` interfaces */
    // this.instance_prop = true;
  }

  static static_prop: boolean = true;
  /* Produce errors at `@Static_Contract` decorator */
  // static static_prop: string = '';

  static isMember(instance: any): boolean {
    if (instance instanceof this) {
      return true;
    }
    return false;
  }
}


const instance = new Instance('spam');
console.log('instance.constructor.isMember(instance) === true', instance.constructor.isMember(instance) === true);
console.log('Instance.isMember(instance) === true ->', Instance.isMember(instance) === true);


/**
 * Allow NodeJS to import or require without breaking web-browser support
 */
if (typeof module !== 'undefined') {
  module.exports = { Instance }
}
```


The _magic_ is how `Static_Contract` is defined and then used via `@Static_Contract<__TYPE__>` which through the use of Generics and extending functions produces a _contract_ that TypeScript can enforce.

It is not nearly as clean as...


```typescript
interface Name {
  static prop: boolean;
}
```


... but it at least functions without breaking anything; or at least I've not found Decorators breaking things, yet.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

