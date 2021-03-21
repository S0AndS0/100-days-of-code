---
layout: post
title: JavaScript Shared Exponent
date: 2021-03-21 15:46:20 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Function that returns scaling exponent to convert list of floats to integers
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---


A common gripe with most programming, and scripting, languages is that floating point calculations have results that initially seem incorrect, eg...


```javascript
console.log(0.1 + 0.2);
//> 0.30000000000000004
```


... Most humans when presented with _`0.1 + 0.2`_ would agree that _`0.3`_ should be the result. Without getting too stuck in the weeds, the discrepancies between computed results is due to conversions between binary and decimal bases.


There are a number of workarounds for this, but one of the simplest options is to _upscale_ all floats to integers, then preforming arithmetic, and finally _downscaling_ the result to a float. For example the previous calculation may be written as...


```javascript
console.log( ((0.1 * 10) + (0.2 * 10)) / 10 );
//> 0.3
```


So long as compo nits are scared by the same amount, this method will work for any floating point number that doesn't have too many _bits_ beyond the decimal point.


Here's a simple function for finding the shared exponent to scale an arbitrary list of floats to integer...


```javascript
function sharedExponent(...args) {
  return args.reduce((accumulator, arg) => {
    const decimal = `${arg}`.split('.')[1];
    if (decimal && decimal.length > accumulator) {
      return decimal.length;
    }
    return accumulator;
  }, 0);
}
```


... and an example usage...


```javascript
{
  const numbers_to_sum = [1.1, 0.02, 3];

  const shared_exponent = sharedExponent(...numbers_to_sum);

  const upscale_numbers = numbers_to_sum.map((n) => {
    return n * (10 ** shared_exponent);
  });

  const upscaled_sum = upscale_numbers.reduce((accumulator, n) => {
    return accumulator + n;
  }, 0);

  const downscaled_sum = upscaled_sum / (10 ** shared_exponent);

  console.log(downscaled_sum);
  //> 4.12
}
```


Beware however, this trick will fail for floating point numbers that are sufficiently complex/long, and the upscaling/downscaling processes may still produce inaccurate results on occasion.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

