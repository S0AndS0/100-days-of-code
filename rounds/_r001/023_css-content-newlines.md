---
layout: post
title: CSS `content` Newlines
date: 2021-01-27 20:59:37 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Inserting newlines in `content` of `::before` and `::after` pseudo elements
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1354662839068274690
  title: Link to Tweet for this post

attribution:
  links:
    - text: Quaxio -- Pure CSS Digital Clock
      href: https://www.quaxio.com/pure_css_digital_clock.html
      title: Pure CSS Digital Clock

    - text: StackOverflow -- Newline character sequence in cSS `content` property
      href: https://stackoverflow.com/questions/9062988/
      title: Newline character sequence in cSS `content` property
      class: fa fa-stack-overflow
---



Recently while dissecting the source code of [Quaxio][link__quaxio__pure_css_digital_clock] I ran across a trick for inserting newlines within the `content` of `::after` and/or `::before` pseudo element(s). Not certain what I'll use it for, but I thought it spiffy enough to warrant sharing with readers here...


---


**`assets/css/main.css`**


```css
.target-class::after {
  content: "First line \a Second line \a Third line";
  white-space: pre;
}
```


**`index.html`**


```html
<div class="target-class"></div>
```


**Example Result**


<style>
.target-class::after {
  content: "First line \a Second line \a Third line";
  white-space: pre;
}
</style>


<div class="target-class"></div>


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__quaxio__pure_css_digital_clock]: {{ page.attribution.links[0].href }} "{{ page.attribution.links[0].title }}"

