---
layout: post
title: JavaScript Decimal Conversion Challenge
date: 2020-06-13 10:15:16 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Coding challenge, convert Decimal integer to another base
time_to_live: 1800
---



Beginner to intermediate challenge. Write a function (without the `toString()` method) that converts Decimal integers to another base, eg...


```javascript
decimalToBase(10, 16);
//> "0xa"

decimalToBase(15, 16);
//> "0xf"
```


... I'll publish my implementation in two weeks.


Hints:


Part `a` of [TutorialsPoint -- How to Convert Decimal to Hexadecimal?](https://www.tutorialspoint.com/how-to-convert-decimal-to-hexadecimal) shows one method with Math to convert integers

While writing your implementation, the `toString()` method can be used to double check results, eg,,,


```javascript
(10).toString(16);
// "a"
```
