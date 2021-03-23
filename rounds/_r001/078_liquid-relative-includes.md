---
layout: post
title: Liquid Relative Includes
date: 2021-03-23 16:25:15 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Gotchas, and workaround, regarding Liquid relative includes
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
    - text: Jekyll -- Includes documentation
      href: https://jekyllrb.com/docs/includes/
      title: Includes documentation
---



Today I learned limitations of the Liquid `include_relative` keyword. Initially I thought the path would be relative to the file calling the keyword, eg...


`_includes/components/other.html`



{% raw %}
```html
<strong>Included component from {{ include.name | default: 'Unknown' }}</strong>
```
{% endraw %}


`_includes/top.html`


{% raw %}
```liquid
<div>
  {% include_relative components/other.html name='top.html' %}
</div>
```
{% endraw %}


`_posts/2021-03-23-include-relative-test.md`


{% raw %}
```markdown
{% include top.html %}
```
{% endraw %}


... However, the above will result in an error similar to...


> `Liquid Exception: Could not locate the included file 'components/other.html' in any of ["~/liquid-utilities/tests/_posts"]. Ensure it exists in one of those directories and, if it is a symlink, does not point outside your site source. in ~/liquid-utilities/tests/_posts/2021-03-23-include-relative-test.md`


Effectively this means that the `include_relative` keyword is relative to the _root_ page/post &#x1F926;


For my use-cases of writing submodules for use in other projects, this makes `include_relative` almost useless, and the only workaround I've found so far is more than a little gross...


{% raw %}
```liquid
{% assign includes_directory = include.includes_directory | default: '' %}

{% capture includes_path %}{{
  includes_directory | append: 'other.html'
}}{% endcapture %}

{% include {{ includes_path }} name='top.html' %}
```
{% endraw %}


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

