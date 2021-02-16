---
layout: post
title: HTML Picture Element
date: 2021-02-14 17:44:21 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick example of utilizing `picture` HTML element
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1361133226438328322
  title: Link to Tweet for this post

attribution:
  links:
    - text: 'MDN -- &lt;picture&gt;: The Picture element'
      href: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture
      title: '&lt;picture&gt;: The Picture element'
      class: fa fa-firefox

    - text: 'MDN -- &lt;img&gt;: The Image Embed element'
      href: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img
      title: '&lt;img&gt;: The Image Embed element'
      class: fa fa-firefox
---



Recently I've been compiling a set of images for sharing on a web based guide, and I read that the HTML5 _`picture`_ element allows compatible browsers to choose an image that is most compatible, eg...


```html
<picture>
  <source type="image/avif" scrset="path/to/image.avif" />
  <source type="image/jpeg" scrset="path/to/image.jpeg" />
  <source type="image/png" scrset="path/to/image.png" />
  <source type="image/webp" scrset="path/to/image.webp" />
  <img alt="Text about image" src="path/to/image.jpeg" />
</picture>
```


... The _`img`_ element is a _fallback_ for browsers that do not support _`picture`_ elements, or when none of the _`source`_ child elements where chosen. Each _`source`_ element may define a _`type`_ and _`srcset`_ attribute, among others, which helps compatible browsers choose an image to download and display.


> Note, check [previous post][link__previous_post] for hints about Linux command-line image format conversions.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

[link__previous_post]: {{ 'r001/040-linux-image-conversion' | abosolute_url }} "Link to post about image format conversion"

