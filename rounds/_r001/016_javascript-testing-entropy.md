---
layout: post
title: JavaScript Testing Entropy
date: 2021-01-20 21:12:50 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Questioning how random `Math.random()` really is
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- 
      href: 
      title: 
      class: fa fa-stack-overflow

    - text: Twitter -- Questions from @nitecoda1 regarding `Math.random()` method
      href: https://twitter.com/nitecoda1/status/1351812896196616192
      title: Questions from @nitecoda1 regarding `Math.random()` method
---



> Questioning how random `Math.random()` really is


---


- [JavaScript Source Code][heading__javascript_source_code]

- [Live Test in This Page][heading__live_test_in_this_page]

- [Explore With Browser Console][heading__explore_with_browser_console]

- [Attribution](#heading__attribution)


---


Today I was question about randomness and chances of collisions; ie. likelyhood that two psudo random numbers are the same...


> [Mark "niteCoda" Freeman -- @nitecoda1](https://twitter.com/nitecoda1/status/1351812896196616192)
>
> ... Is there a way of generating two or more Math.random()...?


So of course I wrote some JavaScript code to stress-test device entropy.


______


## JavaScript Source Code
[heading__javascript_source_code]: #javascript-source-code


Extendable and customizable JavaScript class for checking system entropy...


```javascript
class checkEntropy {
  constructor(delay = 1, random_source = Math.random) {
    this.delay = delay;
    this.random_source = random_source;

    this.a;
    this.b;
  }

  *genRandomPares() {
    while (true) {
      yield [this.random_source(), this.random_source()];
    }
  }

  run() {
    const iterator = this.genRandomPares();
    let count = 0;
    while (count !== Infinity) {
      const id = setTimeout(() => {}, this.delay);
      count++;
      [this.a, this.b] = iterator.next().value;
      if (this.a === this.b) {
        clearTimeout(id);
        break;
      }
    }

    console.log(this);
  }
}
```


______


## Check Entropy Usage
[heading__check_entropy_usage]: #check-entropy-usage


Simplist usage example involves creating a new instance of `checkEntropy` and calling the `.run()` method, eg...


```javascript
const entropy_check = new checkEntropy(1000, Math.random);

entropy_check.run();
```


... which will run until either the `count` reaches `Infinity` or a random pare of numbers colide at the same value.


______


## Live Test in This Page
[heading__live_test_in_this_page]: #live-test-in-this-page


<label for="output-a">A -&gt;</label><input id="output-a" type="text" value="NaN" readonly>

<label for="output-b">B -&gt;</label><input id="output-b" type="text" value="NaN" readonly>

<label for="output-count">Count -&gt;</label><input id="output-count" type="text" value="NaN" readonly>

<label for="output-matched">Matched -&gt;</label><input id="output-matched" type="text" value="false" readonly>

<input id="input-step" type="button" value="Step">


<style>
#output-matched[value="true"] {
  background-color: lightgreen;
}
</style>


<script>
class checkEntropy {
  constructor(delay = 1, random_source = Math.random) {
    this.delay = delay;
    this.random_source = random_source;

    this.a;
    this.b;
  }

  *genRandomPares() {
    while (true) {
      yield [this.random_source(), this.random_source()];
    }
  }

  run() {
    const iterator = this.genRandomPares();
    let count = 0;
    while (count !== Infinity) {
      const id = setTimeout(() => {}, this.delay);
      count++;
      [this.a, this.b] = iterator.next().value;
      if (this.a === this.b) {
        clearTimeout(id);
        break;
      }
    }

    console.log(this);
  }
}


window.addEventListener('load', () => {
  const button_input__step = document.getElementById('input-step');

  let text_output__a = document.getElementById('output-a');
  let text_output__b = document.getElementById('output-b');
  let text_output__count = document.getElementById('output-count');
  let text_output__matched = document.getElementById('output-matched');

  /**
   * Callback function for button 'step'
   */
  button_input__step.addEventListener('click', () => {
    const iterator = new checkEntropy().genRandomPares();
    let count = Number(text_output__count.value) || 0;
    count++;
    text_output__count.value = count;
    [text_output__a.value, text_output__b.value] = iterator.next().value;
    if (text_output__a.value === text_output__b.value) {
      text_output__matched.value = 'true';
    } else {
      text_output__matched.value = 'false';
    }
  });
});
</script>


______


## Explore With Browser Console
[heading__explore_with_browser_console]: #explore-with-browser-console


This page includes within it's source a copy of the above `class`, so readers that are utilizing a compatible web-browser may open the JavaScript console and experiment. Here's a quick list of browsers and the keyboard shortcuts that'll open the console...


- Chrome -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>K</kbd>

- Firefox -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>J</kbd>

- Opera -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd>

- Safari -- <kbd>Cmd</kbd> + <kbd>Opt</kbd> + <kbd>c</kbd>


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

