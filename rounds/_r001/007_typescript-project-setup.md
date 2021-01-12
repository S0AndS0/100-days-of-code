---
layout: post
title: TypeScript Project Setup
date: 2021-01-11 15:23:43 -0800
#date_updated:  # Optional and formatted like 'date' above
description: An outline of steps I use to initialize a new TypeScript project
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https:example.com
  title: Link to Tweet for this post

attribution:
  links:
    - text: JestJS Home Page
      href: https://jestjs.io/
      title: Documentation for Jest JavaScript testing framework
---



An outline of steps I use to initialize a new TypeScript project


---


- [Organization Setup][heading__organization_setup]

- [Git Initialization][heading__git_initialization]

- [Project Directories and Files][heading__project_directories_and_files]

  - [TypeScript Configuration][heading__typescript_configuration]
  - [NPM Configuration Modifications][heading__npm_configuration_modifications]
  - [Script Template][heading__script_template]
  - [Tests Template][heading__tests_template]

- [Git Directories and Files][heading__git_directories_and_files]

- [Publicly Publish][heading__publicly_publish]

- [Questions, Comments, or Suggestions][heading__questions_comments_or_suggestions]

- [Attribution](#heading__attribution)


---


## Organization Setup
[heading__organization_setup]: #organization-setup


GitHub Organizations that I administrate are organized under their own sub-directories, eg...


```bash
mkdir -p ~/git/hub/javasript-utilities

cd ~/git/hub/javasript-utilities
```


---


## Git Initialization
[heading__git_initialization]: #git-initialization


After changing current working directory to the `javasript-utilities` sub-directory creating a new Git repository with a short, and descriptive, name is a good idea. And again the current working directory is changed, this time to the root of the new Git repository...


```bash
git init iterator-chain

cd ~/git/hub/javasript-utilities/iterator-chain
```


---


## Project Directories and Files
[heading__project_directories_and_files]: #project-directories-and-files


Next task is creating directories and files specific to writing TypeScript source code...


```bash
mkdir -p ts/__tests__
touch ts/iterator-chain.ts
touch ts/__tests__/tests-iterator-chain.ts
```


---


### TypeScript Configuration
[heading__typescript_configuration]: #typescript-configuration


For project intended for web-browsers I utilize a TypeScript configuration similar to...


```bash
tee tsconfig.json 1>/dev/null <<'EOF'
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
EOF
```


---


### NPM Configuration Modifications
[heading__npm_configuration_modifications]: #npm-configuration-modifications


Generally I initialize NPM project files via the Q/A built-in helper script...


```bash
npm init
```


... then add common development dependencies...


```bash
npm install --save-dev @types/jest\
                       @types/node\
                       jest\
                       ts-jest\
                       typescript
```


... and finally, for NPM customization, I'll use `"scripts"`, and `"jest"`, configuration keys as shown...


**`package.json` (snip)**


```json
{
  "scripts": {
    "ts-build": "tsc --build",
    "ts-watch": "tsc --watch",
    "ci-test": "jest --coverage",
    "ci-build": "npm run ts-build && npm run ci-test",
    "ci-watch": "jest --coverage --watchAll",
    "py-serve": "python3 -m http.server --bind localhost 8080"
  },
  "jest": {
    "verbose": true,
    "testEnvironment": "jsdom",
    "roots": [
      "__tests__"
    ],
    "collectCoverageFrom": [
      "iterator-chain.js"
    ],
    "coveragePathIgnorePatterns": [
      "node_modules/"
    ],
    "coverageThreshold": {
      "global": {
        "statements": 100,
        "branches": 100,
        "functions": 100,
        "lines": 100
      }
    },
    "coverageReporters": [
      "text"
    ]
  }
}
```


---


### Script Template
[heading__script_template]: #script-template


TypeScript/JavaScript projects that I maintain usually make use of _`class`es_ in order to have a defined _name space_ for methods and functions...


**`ts/iterator-chain.ts`**


```typescript
'use strict';


/**
 * Enables static methods to be called from within class methods
 * @see {link} - https://github.com/Microsoft/TypeScript/issues/3841
 */
interface Iterator_Chain {
  constructor: typeof Iterator_Chain;
}


/**
 *
 */
class Iterator_Chain {

  /**
   *
   */
  constructor() {
  }


  /**
   *
   */
  // fn_name() {}
}


/* istanbul ignore next */
if (typeof module !== 'undefined') {
  module.exports = Iterator_Chain;
}
```


---


### Tests Template
[heading__tests_template]: #tests-template


Test Driven Development is facilitated thanks to JestJS framework...


**`ts/__tests__/test-iterator-chain.ts`**


```typescript
'use strict';


/**
 * Enables static methods to be called from within class methods
 * @see {link} - https://github.com/Microsoft/TypeScript/issues/3841
 */
interface Test__Iterator_Chain {
  constructor: typeof Test__Iterator_Chain;
}


/**
 * Tests methods for instance(s) of `Iterator_Chain` class
 */
class Test__Iterator_Chain {
  iteratorChain: Iterator_Chain;
  iterable: any[];

  constructor(iterable: any[]) {
    this.iterable = iterable;
    this.iteratorChain = require('../iterator-chain');
  }

  /**
   *
   */
  runTests() {
    this.testConstructor();
  }

  /**
   *
   */
  testConstructor() {
    test('constructor -> Defaults are correctly assigned?', () => {
      const iteratorChain = new this.iteratorChain(this.iterable);
      expect(iteratorChain.iterable).toStrictEqual(this.iterable);
    });
  }
}


const iterable = Array(10).fill(0).map((_, i) => i);
const test__iterator_chain = new Test__Iterator_Chain(iterable);
test__iterator_chain.runTests();
```


---


## Git Directories and Files
[heading__git_directories_and_files]: #git-directories-and-files


After writing and testing plugin script(s), and filling-out documentation file(s), it's time to focus on populating Git specific directories and files...


```bash
tee -a .gitignore 1>/dev/null <<'EOF'
*.swp
node_modules
EOF


mkdir .github
touch .github/README.md


touch LICENSE
```


> Note, for most projects I'll utilize the [`github-utilities/make-readme`][link__github_utilities__make_readme] project for starting a formatted `ReadMe` file and choosing a License.


---


## Publicly Publish
[heading__publicly_publish]: #publicly-publish


Once testing and refactoring is complete, the plugin _should_ be ready to publicly publish...


```bash
git checkout -b main


git add .github\
        .gitignore\
        LICENSE\
        ts*\
        package*\
        iterator-chain*\
        __tests__


git commit -F- <<'EOF'
:tada: Initial commit...
EOF


git remote add hub "git@github.com:javasript-utilities/iterator-chain.git"
git push hub main
```

---


## Questions, Comments, or Suggestions
[heading__questions_comments_or_suggestions]: #questions-comments-or-suggestions


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


---


[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

