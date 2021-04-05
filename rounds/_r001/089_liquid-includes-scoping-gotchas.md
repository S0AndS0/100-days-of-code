---
layout: post
title: Liquid Includes Scoping Gotchas
date: 2021-04-03 15:59:36 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Things to keep in mind when writing Liquid includes files
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://twitter.com/S0_And_S0/status/1378483092470575104
  title: Link to Tweet for this post
---


When writing Liquid includes there are a few scoping and output things to keep in mind. First the output of an includes file, including empty spaces and/or new lines will be output unless measures are taken. Second variables assigned within an includes file may overwrite page/post variables.



---


- [Scope Examples][heading__scope_examples]
  - [Example Liquid Includes][heading__example_liquid_includes]
  - [Example MarkDown Post][heading__example_markdown_post]
  - [Example HTML Output (snip)][heading__example_html_output_snip]

- [Commented Code Gotcha][heading__commented_code_gotcha]

- [Contact and/or Contribute][heading__contact_andor_contribute]


---

______


## Scope Examples
[heading__scope_examples]: #scope-examples


To ensure output of an includes file is as small as possible, I like to use `capture` blocks.


And to mitigate overwriting post/page variables, I prefix all variables with `workspace__<includes_name>` and try to _`nil`_ values when finished.


---


### Example Liquid Includes
[heading__example_liquid_includes]: #example-liquid-includes


{% raw %}
```liquid
{% capture workspace__variables %}
{% comment %}
---
vim: filetype=liquid
author: S0AndS0
license: AGPL-3.0
---
{% endcomment %}

{% assign variable_name = 'include value' %}

{% assign workspace__variables__output = variable_name %}

{% endcapture %}{{ workspace__variables__output }}{% assign workspace__variables__output = nil %}
```
{% endraw %}


> Note, in above example the `variable_name` was not set to `nil` prior to ending the includes file!


---


### Example MarkDown Post
[heading__example_markdown_post]: #example-markdown-post


**`2021-04-03-test-variables.md`**


{% raw %}
```markdown
---
author: S0AndS0
title: Test Variables
description: Liquid variable tests
date: 2021-04-03 14:31:00 -0700
layout: post
---


{% assign variable_name = 'post value' %}


variable_name value -> {{ variable_name }}


## Test variable.html scope leak


Include output -> {% include variables.html %}


variable_name value -> {{ variable_name }}
```
{% endraw %}


---


### Example HTML Output (snip)
[heading__example_html_output_snip]: #example-html-output-snip


```html
<p>
  variable_name value -&gt; post value
</p>

<h2 id="test-variablehtml-scope-leak">
  Test variable.html scope leak
</h2>

<p>
 Include output -&gt; include value
</p>

<p>
  variable_name value -&gt; include value
</p>
```


Notice how the value of `variable_name` changed after the included code was executed.


______


## Commented Code Gotcha
[heading__commented_code_gotcha]: #commented-code-gotcha


One final gotcha when using previous coding patterns, `comment` blocks within `capture` blocks may execute code, eg...


**`bad-example.html`**


```liquid
{% capture workspace__example %}
{% comment %}
{% assign commented_variable = 'Uhoh' %}
{% endcomment %}

Content of includes file

commented_variable -&gt; {{ commented_variable }}

{% endcapture %}{{ workspace__example }}{% assign workspace__example = nil %}
```


... When writing comments that demonstrate usage this can cause include files to misbehave.


**`slightly-better-example.html`**


So far the way I've found that mitigates this behaviour is wrapping any commented liquid code within a `raw` block, eg...


```liquid
{% capture workspace__example %}
{% comment %}
{% raw %}
{% assign commented_variable = 'Uhoh' %}
{% endraw %}
{% endcomment %}

Content of includes file

commented_variable -&gt; {{ commented_variable }}

{% endcapture %}{{ workspace__example }}{% assign workspace__example = nil %}
```


... Which seems to cause captured commented code to be ignored by the interpreter.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

