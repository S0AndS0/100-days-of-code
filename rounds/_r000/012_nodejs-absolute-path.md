---
layout: post
title: NodeJS Absolute Path
date: 2020-05-09 09:51:43 -0700
#date_updated:  # Optional and formatted like Sat May  9 09:51:43 PDT 2020 above
description: RegExp incantations for building absolute directory/file paths
time_to_live: 1800
---



Regular Expression incantations for building absolute directory/file paths...


```javascript
#!/usr/bin/env node

'use strict';


const os = require('os');
const path = require('path');


const absPath = (input) => {
  if (input.indexOf('~/') === 0) {
    return input.replace(/^~\//, os.homedir());
  }
  return input.replace(
    new RegExp(`^(?!${path.sep})`),
    `${__dirname}${path.sep}`
  );
};


console.log(absPath('somewhere'));
//> /home/user/<PWD>/somewhere

console.log(absPath('~/elsewhere'));
//> /home/user/elsewhere

console.log(absPath('/home/user/somewhere'));
//> /home/user/somewhere
```


**Notes**


- `new RegExp(...)` seems to be required to reliably detect strings that do **not** begin with `/` or `\`, mainly due to embedding `${path.sep}` within the pattern

- `input.indexOf('~/') === 0` detects Unix/Linux vs MicroSoft paths
