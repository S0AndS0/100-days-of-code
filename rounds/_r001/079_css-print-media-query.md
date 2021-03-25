---
layout: post
title: CSS Print Media Query
date: 2021-03-24 13:34:51 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Some CSS print tips and tricks I've picked-up over the years
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1374503776116084753
  title: Link to Tweet for this post

attribution:
  links:
    - text: MDN -- Using media queries
      href: https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries
      title: Using media queries
      class: fa fa-fire-fox

    - text: MDN -- Attribute selectors
      href: https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors
      title: Attribute selectors
      class: fa fa-fire-fox

    - text: MDN -- page-break-inside
      href: https://developer.mozilla.org/en-US/docs/Web/CSS/page-break-inside
      title: page-break-inside
      class: fa fa-fire-fox

    - text: MDN -- break-inside
      href: https://developer.mozilla.org/en-US/docs/Web/CSS/break-inside
      title: break-inside
      class: fa fa-fire-fox

    - text: MDN -- page-break-after
      href: https://developer.mozilla.org/en-US/docs/Web/CSS/page-break-after
      title: page-break-after
      class: fa fa-fire-fox

    - text: MDN -- break-after
      href: https://developer.mozilla.org/en-US/docs/Web/CSS/break-after
      title: break-after
      class: fa fa-fire-fox
---


One, of many, useful things that CSS `@media` queries allow for are adjusting page styling when a browser prints to PDF, or paper. For example the following set of CSS rules will expose the full path of links...


```css
@media print {
  :root {
    --url-base: "{{ '/' | absolute_url }}";
  }

  /* All links */
  a::after {
    font-size: small;
  }

  /* Internal path links */
  a[href=^"/"]::after {
    content: (var(--url-base)attr(href));
  }

  /* External page links */
  a[href=^"http"]::after {
    content: (attr(href));
  }
}
```


---


An additional set of `print` related tricks I've found useful for various projects, are hinting where page breaks should be placed and avoided...


```css
@media print {
  section p {
    page-break-inside: avoid;
    break-inside: avoid;
  }

  section:not(:last-child) {
    page-break-after: always;
    break-after: always;
  }
}
```


> Note, `section` element targeting may need adjusted depending upon layout/style choices.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

