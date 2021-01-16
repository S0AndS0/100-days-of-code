---
layout: post
title: JavaScript Challenge Sum Parameters
date: 2021-01-04 12:26:21 -0800
#date_updated:  # Optional and formatted like 'date' above
description: JavaScript challenge for readers to find inputs that produce unintended output
time_to_live: 1800

attribution:
  links:
    - text: '@maxherojp of Twitter'
      href: https://twitter.com/maxherojp/status/1345873303379079168
      title: Though similar, in that `.every` and `.reduce` Array methods are used, their handles erroneous input differently

    - text: '@GProgramadora of Twitter'
      url: https://twitter.com/GProgramadora/status/1345478284230987778
      title: What started as a joke inspired the code shared here

tweet:
  url: https://twitter.com/S0_And_S0/status/1346184633180942336
---



The following function attempts to sum an arbitrary number of parameters, by ignoring inputs that are non-numerical...


```javascript
function Sum(...parameters) {
  return parameters.reduce((accumulator, argument) => {
    if (isNaN(argument)) {
      return accumulator;
    }

    let matched = `${argument}`.match(/-?[0-9]\.?/g);
    if (matched === null || matched.join('') != argument) {
      return accumulator;
    }
    return accumulator + Number(argument);

  }, 0);
}
```


Provided that the `Sum()` function operates as intended it should **only** return number typed values; signed or unsigned floats to be specific. If all inputs are not number-like, then `Sum()` _should_ return `0`.


Example inputs and expected behavior...


```javascript
Sum(40, '2');
//> 42

Sum('5', 'ham', -4);
//> 1

Sum('Nutella', 'peanut-butter', 'waffles');
//> 0
```


Unintended behavior may be, but not limited to;


- Return `NaN`

- Return `String` type, or any non-`Number` type object

- Throws an error

