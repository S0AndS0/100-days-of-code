---
layout: post
title: Vim Commented Configurations
date: 2021-03-07 14:49:18 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Configure Vim via script or file comment
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1368357541697253390
  title: Link to Tweet for this post
---



Vim may be configured by the file that is read via `vim: <configurations>` line, for example Vim help files often contain the following line near the end of the document...


```vim
" vim: filetype=help
```


Lately I've found this useful for HTML templates built with Liquid, eg...


**`_layouts/default.html`**


{% raw %}
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>{{ page.title | default: site.title }}</title>
  </head>

  <body>
    {%- include header.html -%}
    <main>
      {{ content }}
    </main>
    {%- include footer.html -%}
  </body>
</html>
{% comment %}
vim: filetype=liquid
{% endcomment %}
```
{% endraw %}


... Because syntax highlighting for both `html` and `liquid` are _activated_ at the same time.


Other, or additional, configurations may be defined as a colon (`:`) separated list. For example to define `textwidth`, `filetype`, and `conceallevel` configurations may be similar to...


**`_posts/example.md`**


```markdown
---
title: Example Post Title
description: Shows how to define Vim configuraiton within FrontMatter
date: 2021-03-07 14:49:18 -0800
vim: textwidth=78:filetype=markdown:conceallevel=1
---
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

