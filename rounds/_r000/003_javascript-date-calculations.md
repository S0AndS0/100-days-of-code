---
layout: post
title: JavaScript Date Calculations
date: 2020-04-30 11:26:25 -0700
#date_updated:  # Optional and formatted like Thu Apr 30 11:26:25 PDT 2020 above
description: Hacking time with JavaScript
time_to_live: 1800
---



Calculating with JavaScript when `#100DaysofCode` is finished...


```javascript
/**
 * Customized object returned by `formatDate` function
 * @typedef {Object} formattedDate
 * @property {number} year
 * @property {number} month
 * @property {number} day
 */


/**
 * Returns date object offset by number of days provided
 * @param {number} days - Amount of days to add (or subtract) to current time
 * @returns {Date}
 */
const addDays = (days) => {
  const date = new Date();
  date.setDate(date.getDate() + days);
  return date;
};


/**
 * Offsets month and zero-pads both month and day
 * @param {Date} date - Date object to format and return as dictionary
 * @returns {formattedDate}
 */
const formatDate = (date) => {
  return {
    year: date.getFullYear(),
    month: ("0" + (date.getMonth() + 1)).slice(-2),
    day: ("0" + date.getDate()).slice(-2)
  };
}


const formattedDate = formatDate(addDays(100));

console.log(`${formattedDate.year}-${formattedDate.month}-${formattedDate.day}`);
//> 2020-08-08
```


... JavaScript has _interesting_ ideas when it comes to dealing with time;


- `getMonth()` is zero indexed, meaning that months range from `0` to `11`

- `getDay()` returns the day of the week, Sunday starting at `0`

- `getDate()` returns the day of the month, starting at `1`

- padding numbers with zeros requires converting to a string, then slicing the length desired


___


## Attribution


- [StackOverflow -- How do I get month and date of JavaScript in 2 digit format](https://stackoverflow.com/questions/6040515/)

- [StackOverflow -- JSDoc return object structure](https://stackoverflow.com/questions/28763257/)
