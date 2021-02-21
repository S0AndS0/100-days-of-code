---
layout: post
title: CSS HTML Image Aspect Ratio
date: 2021-02-19 18:56:11 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Tips on preventing image _squeeze_ when view port is less-than image width
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1363006527557238786
  title: Link to Tweet for this post
---



For the tutorial that I published this week I wanted to have images resize if the view-port was less than the image width, but I also wanted to maintain the aspect ratio. Thankfully CSS is able to achieve this when HTML attributes are defined too.


Here's some example HTML...


```html
<img alt-text="Place holder image of a cat"
     width="700"
     height="500"
     src="https://placekitten.com/700/500" />
```


... A bit of CSS that do the _magic_...


```css
img {
  max-width: 100%;
  height: auto;
}
```


... And example results...


<style>
img {
  max-width: 100%;
  height: auto;
}
</style>

<img alt-text="Place holder image of a cat"
     width="700"
     height="500"
     src="https://placekitten.com/700/500" />


If viewing on a web-browser capable of resizing the view port, then attempt to shrink the width and the height of above image _should_ automatically adjust.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

