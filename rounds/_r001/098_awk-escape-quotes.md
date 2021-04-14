---
layout: post
title: Awk Escape Quotes
date: 2021-04-12 15:36:36 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Few gotchas and tips regarding quotes within Awk scripts and commands
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1381739505376505858
  title: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- How to escape a single quote inside awk
      href: https://stackoverflow.com/questions/9899001/
      title: How to escape a single quote inside awk
      class: fa fa-stack-overflow
---



It may be totally subjective, but it feels like every few weeks I need to escape single-quotes within some pipe-line or script that utilizes Awk for parsing. What's more is that how to escape single-quotes changes depending on if Awk is run from a script or via terminal prompt.


As a simple example the following detects, and reports, if read lines begin with a single-quote (`'`)...


```bash
awk '{
  if ($0 ~ "^'\''") {
    print "Yep";
  } else {
    print "Nope";
  }
}' <<EOF
'foo
bar
EOF
```


The first single-quote (_`awk '{...`_) starts a string for Awk to interpret; ie Bash, or whatever parent shell, generally should **not** attempt to expand string within single quotes.


The second single-quote (_`if ($0 ~ "'...`_) temporally pauses Awk interpreting and allows the parent shell to inject characters.


> Note this is also a method to inject variables or sub-shell output directly into Awk, though I cannot recommend it.


The third single-quote (_`...\'...`_) is a literal single-quote.


The forth single-quote (_`...'") {...`_) resumes defining commands for Awk to interpret, and things move along as usual.


In short `'\''` is the _magic incantation_ that allows for injecting single-quotes within Awk, and other similar scripting languages.


---


While the above functions nicely for quick _one-off_ Awk parsing, writing scripts for later reuse requires a different set of syntax...


**`leading-single-quotes.awk`**


```awk
#!/usr/bin/awk -f

BEGIN {
  SINGLE_QUOTE = "'";
  PATTERN = "^" SINGLE_QUOTE;
}

{
  if ($0 ~ PATTERN) {
    print "Yep";
  } else {
    print "Nope";
  }
}
```


Bare single-quotes are not allowed, eg...

    DOUBLE_QUOTE = '"'

... will produce an error, because single-quotes are _special_ in Awk. However, escaping and/or matching double-quotes within scripts is somewhat simpler...


**`double-quotes.awk`**


```awk
#!/usr/bin/gawk -f


BEGIN {
  DOUBLE_QUOTE = "\"";
  PATTERN = "^" DOUBLE_QUOTE;
}

{
  if ($0 ~ PATTERN) {
    print "Yep";
  } else {
    print "Nope";
  }
}
```


... Better still, double-quote escapement operates the same regardless of if executed as a script or apart of a shell pipe-line.


---


**Example execution**


```bash
leading-single-quotes.awk <<EOF
'foo
bar
EOF
```


---


**Example output**


```
#> Yep
#> Nope
```

______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

