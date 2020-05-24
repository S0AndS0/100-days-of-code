---
layout: post
title: JavaScript 2D Element Matrix
date: 2020-05-24 10:23:56 -0700
#date_updated:  # Optional and formatted like Sun May 24 10:23:56 PDT 2020 above
description: An example of using `Array(_n_).fill()` and `Array.map()`
time_to_live: 1800
---



JavaScript function that returns 2D matrix of HTML elements...


```javascript
function htmlMatix(size, tag_name = 'div') {
  return Array(size).fill().map((_row, y) => {
    return Array(size).fill().map((_cell, x) => {
      const element = document.createElement(tag_name);
      element.id = `{"${tag_name}": {"x": ${x}, "y": ${y}}}`;
      return element;
    });
  });
}
```


> Note, `Array(_n_).fill()` is _lazy_ in that it will reuse references to nodes and/or objects, which is why `Array.map()` is used immediately after to return arrays with unique element references.


Example usage...


```javascript
// Ensure that a container is available
let container;
if (document.getElementById('container')) {
  container = document.getElementById('container');
} else {
  container = document.createElement('div');
  document.body.appendChild(container);
}

// Empty container element
container.innerHTML = '';

// Create and customize element matrix
const div_matrix = htmlMatix(3, 'div');

div_matrix.forEach((row) => {
  row.forEach((cell) => {
    const coordinates = cell.id;
    const tag_name = cell.tagName.toLowerCase();
    console.log(`Appending ${tag_name} with id ${coordinates} to container`);
    container.appendChild(cell);
  });
});
// Appending div with id {"div":{"x":0,"y":0}} to container
// Appending div with id {"div":{"x":1,"y":0}} to container
// Appending div with id {"div":{"x":2,"y":0}} to container
// Appending div with id {"div":{"x":0,"y":1}} to container
// ...
```
