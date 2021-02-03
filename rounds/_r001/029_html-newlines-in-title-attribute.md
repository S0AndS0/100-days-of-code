---
layout: post
title: HTML Newlines in Title Attribute
date: 2021-02-02 21:50:05 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Inserting newlines within link on-hover text for MarkDown or HTML documents
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
    - text: StackOverflow -- How can I add new line/linebreak character in title attribute in HTML
      href: https://stackoverflow.com/questions/18606877/
      title: How can I add new line/linebreak character in title attribute in HTML
      class: fa fa-stack-overflow
---



While writing documentation for a project I had the want for newlines within on-hover text for links. MarkDown syntax for building reference is similar to...


```markdown
[Clickable Text][link__to_somewhere]

[link__to_somewhere]: https://example.com
```


... which generates HTML similar to...


```html
<a href="https://example.com">Clickable Text</a>
```


**Example Result**


<a href="https://example.com">Clickable Text</a>


---


Adding on-hover text within MarkDown documents is accomplished by adding a quoted string after the URL, eg...


```markdown
[Clickable Text][link__to_somewhere]

[link__to_somewhere]: https://example.com "Text to show on-hover"
```


... that is then parsed to HTML sorta like...


```html
<a href="https://example.com"
   title="Text to show on-hover"
   >Clickable Text</a>
```


**Example Result**


<a href="https://example.com" title="Text to show on-hover">Clickable Text</a>


---


But I wanted to have multiple lines of formatted text within the on-hover string, the `&#10;` Unicode is what I found to do just that; again in MarkDown that'd be written as...


```markdown
[Clickable Text][link__to_somewhere]

[link__to_somewhere]: https://example.com "First line&#10;Second line&#10;Third line"
```


... which is transpiled to HTML such as...


```html
<a href="https://example.com"
   title="First line&#10;Second line&#10;Third line"
   >Clickable Text</a>
```


**Example Result**


<a href="https://example.com" title="First line&#10;Second line&#10;Third line">Clickable Text</a>


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__quaxio__pure_css_digital_clock]: {{ page.attribution.links[0].href }} "{{ page.attribution.links[0].title }}"

