---
layout: post
title: CSS counter and checkbox gotcha
date: 2020-05-19 16:16:26 -0700
#date_updated:  # Optional and formatted like Tue May 19 16:16:26 PDT 2020 above
description: '`counter-increment` reverts if checkbox state reverts'
time_to_live: 1800
---



The goal is to increment `score` counter every time a checkbox is checked, however tests show that `counter-increment` reverts if checkbox state reverts...


**`index.html`**


```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Limitations of checkbox and counter-increment</title>
    <link rel="stylesheet" href="main.css">
  </head>


  <body>
    <input type="checkbox" class="checkbox--hidden" id="checkbox--add-to-score">
    <input type="checkbox" class="checkbox--hidden" id="checkbox--reset-score">

    <div class="game-container">

      <div class="inputs-container">
        <label class="label--clickable label--reset-score" for="checkbox--reset-score">Reset Score</label>
        <label class="label--clickable label--add-to-score" for="checkbox--add-to-score">Click Me!</label>
      </div>

      <div class="score-container">
        <span class="span--score">Score</span>
      </div>

    </div>
  </body>
</html>
```


**`main.css`**


```css
.checkbox--hidden {
  display: none;
  visibility: hidden;
  opacity: 0;
  filter: alpha(opacity=0); /* Old Microsoft opacity */
}

.score-container {
  height: 10vh;
  margin-bottom: 15px;
  font-size: 30px;
  line-height: 2;
  min-height: 40px;
  background-color: lightyellow;
  text-align: center;
}

.label--clickable,
.span--score {
  padding: 15px;
  margin: 15px;
}

.label--clickable {
  border-radius: 25%;
  font-size: 20px;
  line-height: 2;
  min-height: 20px;
  min-width: 40px;
}

.label--add-to-score{
  background-color: lightgreen;
  float: right;
}

.label--reset-score {
  background-color: pink;
  float: left;
}

.score-container {
  counter-reset: score 0;
}


/* Dynamic CSS stuff */


input[id="checkbox--add-to-score"]:checked ~ .game-container .span--score {
  counter-increment: score 1;
}

input[id="checkbox--reset-score"]:checked ~ .game-container .span--score {
  counter-reset: score;
}

.span--score::after {
  content: ": " counter(score);
}
```


... feel free to let me know via Twitter or a Pull Request if there is a solution, or if this is simply not possible with CSS and HTML alone.
