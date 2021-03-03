---
layout: post
title: JavaScript Fonts Ready
date: 2021-03-02 17:00:30 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Experimental script for detecting when fonts are ready/loaded
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1366924312775647233
  title: Link to Tweet for this post

attribution:
  links:
    - text: CSS Tricks -- The Best Font Loading Strategies and How to Execute Them
      href: https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/
      title: The Best Font Loading Strategies and How to Execute Them
      class: fa fa-CSS3

    - text: CSS Wizardry -- The Fastest Google Fonts
      href: https://csswizardry.com/2020/05/the-fastest-google-fonts/
      title: The Fastest Google Fonts
      class: fa fa-CSS3
---



I've been working on a custom Jekyll theme that will utilize custom fonts, which lead to doing much research for such developments. The following JavaScript is **experimental**, but _should_ allow enable detection of when fonts have loaded...


**`assets/javascript/load-font.js`**


```javascript
'use strict';


function loadFonts() {
  if (sessionStorage.fontsLoaded) {
    document.documentElement.classList.add('fonts-loaded');
    return;
  }

  document.fonts.ready.then(_ => {
    document.documentElement.classList.add('fonts-loaded');
    sessionStorage.fontsLoaded = true;
  });
}


window.addEventListener('load', () => {
  loadFonts();
});
```


Provided that above functions as intended, the following CSS _should_ gracefully switch to `custom-font` when the `fonts-loaded` class is added...


**`assets/css/main.css` (snip)**


```css
body {
  font: -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        "Segoe UI Symbol",
        "Segoe UI Emoji",
        "Apple Color Emoji",
        Roboto,
        Helvetica,
        Arial,
        sans-serif;
}


.fonts-loaded body {
  font: custom-font,
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        "Segoe UI Symbol",
        "Segoe UI Emoji",
        "Apple Color Emoji",
        Roboto,
        Helvetica,
        Arial,
        sans-serif;
}
```


Now for any of the above to function requires that `custom-font` is defined via `@font-face`, eg...


**`assets/css/custom-font.css`**


```css
@font-face {
  font-family: custom-font;
  font-display: swap;
  src: url('assets/fonts/custom-font.otf') format('opentype');
  src: url('assets/fonts/custom-font.woff') format('woff'),
       url('assets/fonts/custom-font.woff2') format('woff2'),
       url('assets/fonts/custom-font.eot');
  font-style: normal;
  font-weight: normal;
}

@font-face {
  font-family: custom-font;
  font-display: swap;
  src: url('assets/fonts/custom-font.otf') format('opentype');
  src: url('assets/fonts/custom-font.woff') format('woff'),
       url('assets/fonts/custom-font.woff2') format('woff2'),
       url('assets/fonts/custom-font.eot');
  font-style: bold;
  font-weight: normal;
}

@font-face {
  font-family: custom-font;
  font-display: swap;
  src: url('assets/fonts/custom-font.otf') format('opentype');
  src: url('assets/fonts/custom-font.woff') format('woff'),
       url('assets/fonts/custom-font.woff2') format('woff2'),
       url('assets/fonts/custom-font.eot');
  font-style: italic;
  font-weight: normal;
}

@font-face {
  font-family: custom-font;
  font-display: swap;
  src: url('assets/fonts/custom-font.otf') format('opentype');
  src: url('assets/fonts/custom-font.woff') format('woff'),
       url('assets/fonts/custom-font.woff2') format('woff2'),
       url('assets/fonts/custom-font.eot');
  font-style: bold;
  font-weight: italic;
}
```


... And this also requires the HTML file(s) to load style sheets and JavaScript(s) correctly...


```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Example Custom Fonts</title>

    <link rel="stylesheet" href="assets/css/main.css">

    <link rel="stylesheet"
          href="assets/css/custom-font.css"
          media="print"
          onload="this.media='all'">

    <script src="assets/js/load-fonts.js" defer></script>
  </head>


  <body>
    <p>Example content</p>
  </body>
</html>
```


> Note, the above _`media="print"`_ combined with _`onload="this.media='all'"`_ trick causes browsers to load the `custom-fonts.css` file at a much lower priority.
>
> And the _`defer`_ attribute causes supported browsers to download JavaScript in the background, but once downloaded execute in a defined order.


There are many moving parts in above examples, but if I've understood everything so far the order _should_ be similar to;


- Load content with `main.css` styling

- Download `custom-fonts.css` asynchronously with a low priority
  - When `custom-font.css` finishes downloading switch media type from `"print"` to `"all"`

- Download `load-font.js` asynchronously
  - When `load-font.js` finishes downloading, and document is fully loaded, add flag to session storage and class to `body` element

- Finally when `.fonts-loaded body` is _true_ the `custom-font` settings are applied


Which _should_ deliver content to clients quickly, while allowing customization/enhancement(s) to take effect only after such things have downloaded.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

