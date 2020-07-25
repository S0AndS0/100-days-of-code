---
layout: post
title: JavaScript character counting function
date: 2020-07-13 12:04:24 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `Array.reduce()` to count characters in a string
time_to_live: 1800
category: javascript
---



Example functions for using `Array.reduce()` to count characters in a string...


{% raw %}
```javascript
/**
 * Builds object of characters and frequency of occurrence from provided string
 * @function characterCounts
 * @param {string} input - eg. 'hook'
 * @return {{ [key: string]: number; }} - eg. {h: 1, o: 2, k: 1}
 */
const characterCounts = (input) => {
  return [...input].reduce((accumulator, character) => {
    accumulator[character]? accumulator[character]++: accumulator[character] = 1;
    return accumulator;
  }, {});
};


/**
 * Builds tuple of key with highest value from provided object
 * @function mostFrequentCharacter
 * @param {{ [key: string]: number; }} character_counts - eg. {h: 1, o: 2, k: 1}
 * @return {{ [index: number]: number|string; }} - eg. ['o', 2]
 */
const mostFrequentCharacter = (character_counts) => {
  return Object.entries(character_counts).reduce((accumulator, [key, value]) => {
    if (!accumulator.length || accumulator[1] < value) {
      accumulator[0] = key;
      accumulator[1] = value;
    }
    return accumulator;
  }, []);
};
```
{% endraw %}


Example usage...


```javascript
const character_counts = characterCounts('spam flavored ham');
const most_frequent_character = mostFrequentCharacter(character_counts);


console.log(most_frequent_character[0]);
//> a

console.log(most_frequent_character[1]);
//> 3
```
