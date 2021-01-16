---
layout: post
title: HTML Quote Elements
date: 2021-01-14 17:31:39 -0800
#date_updated:  # Optional and formatted like 'date' above
description: 'Notes, and examples, for `<q>` and `<blockquote>` HTML elements'
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1349963729346174976
  title: Link to Tweet for this post

attribution:
  links:
    - text: "CSS Tricks -- Quotes Properties"
      href: https://css-tricks.com/almanac/properties/q/quotes/
      title: "CSS Quote Properties"

    - text: "MDN -- &lt;q&gt;: The Inline Quotation element"
      href: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/q
      title: "<q>: The Inline Quotation element"
      class: fa fa-firefox

    - text: "MDN -- &lt;blockquote&gt;: The Block Quotation element"
      href: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote
      title: "<blockquote>: The Inline Quotation element"
      class: fa fa-firefox

    - text: "StackOverflow -- Using css :before and :after pseudo-elements with inline CSS?"
      href: https://stackoverflow.com/questions/14141374/
      title: "Using css :before and :after pseudo-elements with inline CSS?"
      class: fa fa-stack-overflow
---



Prior to this week whenever quoting someone I'd utilize MarkDown syntax to render a `blockquote` element, eg...


**MarkDown Source (snip)**


```markdown
> @Someone
>
> Something about some thing
```


**Example Results**


> @Someone
>
> Something about some thing


... Or in desperation, manually define a HTML `blockquote` element with `cite` attribute...


**HTML Source (snip)**


```html
<blockquote cite="Someone">
  Something about some thing
</blockquote>
```


**Example Results**


<blockquote cite="Someone">
  Something about some thing
</blockquote>


---


But while reading through the MDN documentation, as one does, I read that there be a `q` element; which is intended for inline quoting/citing, eg...


**HTML Source (snip)**


```html
<p>
  I heard someone say,
  <q>Something about some thing</q>
  , which was totally life changing!
</p>
```


**Example Results**


I heard someone say, <q>Something about some thing</q>, which was totally life changing!


---


Combined with some CSS trickery for populating pseudo-element content from HTML attributes, the `<q>` element may have some spiffy uses...


**CSS Source (snip)**


```css
q {
  quotes: "“" "”" "‘" "’";
}

q[cite]::before {
  content: open-quote;
  font-style: italic;
  color: #A9B0BB;
}

q[cite]::after {
  content: close-quote " " attr(cite);
  font-style: italic;
  color: #A9B0BB;
}
```


**HTML Source (snip)**

```html
<p>
  I heard someone say,
  <q cite="Smarty Pants">Something about some thing</q>
  , which was totally life changing!
</p>
```

**Example Results**

<style>
q {
  quotes: "“" "”" "‘" "’";
}

q[cite]::before {
  content: open-quote;
  font-style: italic;
  color: #A9B0BB;
}

q[cite]::after {
  content: close-quote " " attr(cite);
  font-style: italic;
  color: #A9B0BB;
}
</style>

I heard someone say, <q cite="Smarty Pants">Something about some thing</q>, which was totally life changing!


---


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


---



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

