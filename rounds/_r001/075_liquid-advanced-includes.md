---
layout: post
title: Liquid Advanced Includes
date: 2021-03-20 16:53:05 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Quick tips on dynamic and nested includes with Jekyll flavored Liquid
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1373423678764027907
  title: Link to Tweet for this post

attribution:
  links:
    - text: Jekyll -- Includes documentation
      href: https://jekyllrb.com/docs/includes/
      title: Includes documentation
---



Today I learned that Liquid includes files may include other includes &#x1F92F; ... Furthermore the `include` keyword, at least for Jekyll flavored Liquid, allows for a variable target path &#x1F92F;


These features allow for truly utilizing includes similar to function definitions as well as more dynamic theme code.



---


- [`_includes` Directory][heading___includes_directory]

- [`_posts` Directory][heading___posts_directory]

- [HTML Results][heading__html_results]

- [Contact and/or Contribute][heading__contact_andor_contribute]

- [Attribution](#heading__attribution)


---



## `_includes` Directory
[heading___includes_directory]: #_includes-directory


**`source-other.html`**


{% raw %}
```liquid
{% assign target = include.target | default: 'other.html' %}
{% include {{ target }} variable=include.variable %}
```
{% endraw %}


**`other.html`**


{% raw %}
```liquid
{% assign other_variable = include.variable | default: 'Nope' %}
<p>Other Variable: {{ other_variable }}</p>
```
{% endraw %}



**`something.html`**


{% raw %}
```liquid
{% assign other_variable = include.variable | default: 'Nope' %}
<p>Something Variable: {{ other_variable }}</p>
```
{% endraw %}


______


## `_posts` Directory
[heading___posts_directory]: #_posts-directory


**`2021-03-21-tests-nested-includes-one.md` (snip)**


{% raw %}
```markdown
{% include source-other.html %}
```
{% endraw %}


**`2021-03-21-tests-nested-includes-two.md` (snip)**


{% raw %}
```markdown
{% include source-other.html variable='Yep' %}
```
{% endraw %}


**`2021-03-21-tests-nested-includes-three.md` (snip)**


{% raw %}
```markdown
{% include source-other.html variable='Yep' target='something.html' %}
```
{% endraw %}


______


## HTML Results
[heading__html_results]: #html-results


**`2021/03/21/tests-nested-incudes-one.html` (snip)**


```html
<p>Other Variable: Nope</p>
```


**`2021/03/21/tests-nested-incudes-two.html` (snip)**


```html
<p>Other Variable: Yep</p>
```


**`2021/03/21/tests-nested-incudes-three.html` (snip)**


```html
<p>Something Variable: Yep</p>
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

