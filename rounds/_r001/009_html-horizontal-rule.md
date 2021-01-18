---
layout: post
title: HTML Horizontal Rule
date: 2021-01-13 20:02:21 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Tips regarding `<hr>` HTML element style
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1349182987674521602
  title: Link to Tweet for this post

attribution:
  links:
    - text: "MDN -- &lt;hr&gt;: The Thematic Break (Horizontal Rule) element"
      href: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr
      title: "<hr>: The Thematic Break (Horizontal Rule) element"
      class: fa fa-firefox
---



Today I invested some time into proofreading the code, and content, of a stranger's portfolio on GitHub. It somewhat of a palate cleanser from the strongly typed languages I've been writing in as of late, and while researching proofread changes I learned some tricks from the Mozilla Developer Network on how to style `<hr>` (Horizontal Rule) HTML elements with CSS.


Generally horizontal rule elements are placed between paragraphs and/or sections of content, and provide a visual cue to readers that is stronger than a `<br>` (Break) element, eg...


**HTML Source (snip)**


```html
<p>Some content</p>
<hr>
<p>Other content</p>
```


**Example results**

Some content
<hr>
Other content


... When combined with CSS it be possible to explicitly define how _strong_ the visual cue should be...


**CSS Source (snip)**


```css
hr {
  border: none;
  border-top-style: dashed;
  border-top-width: 0.2em;
  border-top-color: #333;
  overflow: visible;
  text-align: center;
  height: 0.7em;
}
```


**Example results**


Some content
<hr style="
  border: none;
  border-top-style: dashed;
  border-top-width: 0.2em;
  border-top-color: #333;
  overflow: visible;
  text-align: center;
  height: 0.7em;
">
Other content


... The _magic_ is defining `border: none;` then overriding `boarder-top-<prop>` properties, and assigning a `height` that isn't too terrible'. Check [MDN -- border-top](https://developer.mozilla.org/en-US/docs/Web/CSS/border-top) for details and how to define properties in a more concise format.


---


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


---


[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

