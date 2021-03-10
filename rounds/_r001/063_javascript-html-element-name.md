---
layout: post
title: JavaScript HTML Element Name
date: 2021-03-08 17:24:52 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick tip for obtaining HTML element name via JavaScript
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1369113363205087233
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- What is the JSDoc type for document `getElementById` and a JQuery Element?
      href: https://stackoverflow.com/questions/18784581/
      title: What is the JSDoc type for document `getElementById` and a JQuery Element?
      class: fa fa-stack-overflow
---



Some of the TypeScript projects that I maintain use HTML element type hints, and recently I found that it is possible to obtain element types via JavaScript console.


For example suppose the following HTML elements are used somewhere within a web-app...


```html
<input id="some-button" type="button" value="Clicky">

<a href="#" id="link-to-somewhere" target="_blank">
  Link to Somewhere
</a>
```


Web-browser JavaScript console may be used to obtain types for each element...


```javascript
document.getElementById('some-button').constructor.name;
//> HTMLInputElement

document.getElementById('link-to-somewhere').constructor.name;
//> HTMLAnchorElement
```


Alternatively leveraging `document.createElement` it's possible to obtain types for common tag element names, eg...


```javascript
document.createElement('button').constructor.name;
//> HTMLButtonElement
```


This `constructor.name` trick may also be used to inspect element event types, eg...


```javascript
const input = document.createElement('button');

input.addEventListener('click', (event) => {
  console.log('Event type ->', event.constructor.name);
});

input.click();
//> Event type -> MouseEvent
```


Combining these tricks it is possible to _hint_ to TypeScript what element, and event, type(s) are expected, eg...


```typescript
function attach_button_listener(
    element: HTMLInputElement | HTMLButtonElement,
    callback: (event?: MouseEvent) => any,
) {
  return element.addEventListener('click', callback);
}
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

