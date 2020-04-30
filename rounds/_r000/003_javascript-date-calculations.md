---
layout: post
title: JavaScript Date Calculations
date: 2020-04-30 11:26:25 -0700
#date_updated:  # Optional and formatted like Thu Apr 30 11:26:25 PDT 2020 above
description: Hacking time with JavaScript
time_to_live: 1800
---



Calculating with JavaScript when `#100DaysofCode` is finished...


```JavaScript
const addDays = (days) => {
  const date = new Date();
  date.setDate(date.getDate() + days);
  return date;
};


const date = addDays(100);


const formattedDate = {
  year: date.getFullYear(),
  month: ("0" + (date.getMonth() + 1)).slice(-2),
  day: ("0" + date.getDate()).slice(-2)
};


console.log(`${formattedDate.year}-${formattedDate.month}-${formattedDate.day}`);
```


... JavaScript has _interesting_ ideas when it comes to dealing with time;


- `getMonth()` is zero indexed, meaning that months range from `0` to `11`

- `getDay()` returns the day of the week, Sunday starting at `0`

- `getDate()` returns the day of the month, starting at `1`

- padding numbers with zeros requires converting to a string, then slicing the length desired


___


## Attribution


- [How do I get month and date of JavaScript in 2 digit format](https://stackoverflow.com/questions/6040515/)
