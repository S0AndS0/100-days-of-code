---
layout: post
title: TypeScript Static Methods
date: 2021-01-18 21:51:20 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Some gotchas, and workarounds, regarding static class methods and TypeScript
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post

attribution:
  links:
    - text: GitHub -- `Microsoft/TypeScript` -- T.constructor should be of type T
      href: https://github.com/Microsoft/TypeScript/issues/3841
      title: T.constructor should be of type T

    - text: StackOverflow -- Interfaces with construct signatures not type checking
      href: https://stackoverflow.com/questions/12952248/
      title: Interfaces with construct signatures not type checking
      class: fa fa-stack-overflow
---



> Some gotchas, and workarounds, regarding static class methods and TypeScript


---


- [Example `interface` for Classes][heading__example_interface_for_classes]

  - [Explanation of `new` Definition][heading__explanation_of_new_definition]
  - [Explanation of `constructor` Definition][heading__explanation_of_constructor_definition]
  - [Explanation of `stMethod` Definition][heading__explanation_of_stmethod_definition]

- [Fully Functional TypeScript Example][heading__fully_functional_typescript_example]

- [Example Configurations][heading__example_configurations]

- [Contact and/or Contribute][heading__contact_andor_contribute]

- [Attribution](#heading__attribution)


---


## Example `interface` for Classes
[heading__example_interface_for_classes]: #example-interface-for-classes


Use the following `interface` as a template for classes to avoid some annoying TypeScript errors...


```typescript
interface CName {
  new(...args: any[]): CName;
  constructor: typeof CName;
  stMethod(...args: any[]): string;
}
```

... Here's a stripped-down `CName` class that will be built upon with the above `interface`...


```typescript
class CName {
  value: any;

  constructor(value: any) {
    this.value = value;
  }

  static stMethod(...args: any[]): string {
    return args.join(' ');
  }
}
```


---


### Explanation of `new` Definition
[heading__explanation_of_new_definition]: #explanation-of-new-definition


Without `new(...args: any[]): CName` errors similar to the following will pop when instantiating a new instance indirectly...


```
This expression is not constructable.   Type 'CName' has no construct signatures.
```


... But with a `new` method signature defined it be possible to invoke new class instances from within another function, or class method, eg...


```typescript
class CIndirect {
  cls: CName;

  constructor(cls: CName) {
    this.cls = cls;
  }

  buildCName(value: any): CName {
    return new this.cls(value);
  }
}
```


---


### Explanation of `constructor` Definition
[heading__explanation_of_constructor_definition]: #explanation-of-constructor-definition


Without `constructor: typeof CName` errors similar to the following will pop...


```
Property 'stMethod' does not exist on type 'Function'
```


... However, with `constructor` defined utilizing static methods within non-static methods of the same class be possible via _`this.constructor.<method-name>`_ syntax, eg...


```typescript
class CName {
  value: any;

  constructor(value: any) {
    this.value = value;
  }

  static stMethod(...args: any[]): string {
    return args.join(' ');
  }

  inMethod(...args: string[]) {
    const message_words = [
      'Something',
      'about',
      'some',
      'thing',
    ];

    console.log(this.constructor.stMethod(message_words));
  }
}
```


---


### Explanation of `stMethod` Definition
[heading__explanation_of_stmethod_definition]: #explanation-of-stmethod-definition


Without `stMethod(...args: any[]): string` errors similar to the following will pop...


```
Property 'stMethod' is a static member of type 'CName'
```


... But by defining `stMethod` within the `interface` no errors are generated from calling from another class indirectly via `this.cls.stMethod` path, it similar to...


```typescript
class CIndirect {
  cls: CName;

  constructor(cls: CName) {
    this.cls = cls;
  }

  executeCNameStatic() {
    return this.cls.stMethod('Spam', 'Flavored', 'Ham');
  }
}
```


______


## Fully Functional TypeScript Example
[heading__fully_functional_typescript_example]: #fully-functional-typescript-example


Consolidating above examples resembles the following TypeScript code...


```typescript
interface CName {
  new(...args: any[]): CName;
  constructor: typeof CName;
  stMethod(...args: any[]): string;
}


class CName {
  value: any;

  constructor(value: any) {
    this.value = value;
  }

  static stMethod(...args: any[]): string {
    return args.join(' ');
  }

  inMethod(...args: string[]) {
    const message_words = [
      'Something',
      'about',
      'some',
      'thing',
    ];

    console.log(this.constructor.stMethod(message_words));
  }
}


class CIndirect {
  cls: CName;

  constructor(cls: CName) {
    this.cls = cls;
  }

  buildCName(value: any): CName {
    return new this.cls(value);
  }

  executeCNameStatic() {
    return this.cls.stMethod('Spam', 'Flavored', 'Ham');
  }
}
```


______


## Example Configurations
[heading__example_configurations]: #example-configurations


For completeness the following `tsconfig.json` file settings where defined for testing the above examples...


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


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

