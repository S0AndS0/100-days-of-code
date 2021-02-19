---
layout: post
title: Bash Parse Image Metadata
date: 2021-02-17 17:14:04 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of utilizing `exiftool` and Vim macros for formatting script output
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1362214571470168064
  title: Link to Tweet for this post
---



Today I invested some time into writing a Bash script for parsing metadata returned by `exiftool`...


**`image-dimensions.sh`**


```bash
#!/usr/bin/env bash


_image_path="${1:?No image path provided}"

[[ -f "${_image_path}" ]] || {
  printf >&2 'Path is not a file -> %s\n' "${_image_path}"
  exit 1
}

exiftool -S "${_image_path}" | awk '{
  _line = tolower($0);
  if (_line ~ "imagewidth") {
    _width = $2;
  } else if (_line ~ "imageheight") {
    _height = $2
  }

  if (_width && _height) {
    print "width=\"" _width "\"";
    print "height=\"" _height "\"";
    exit 0;
  }
}'
```


Example usage...


```bash
./image-dimensions.sh path/to/image.png
#> width="800"
#> height="600"
```


The above script was written because a guide I'll be publishing tomorrow has many print-screen images, and utilizing Vim Ex commands similar to the following enabled me to quickly insert HTML attributes for each image...


```vim
:read !./image-dimensions.sh path/to/image.png
```


**Example HTML snip (before)**


{% raw %}
```html
<picture>
  <!-- ... Other source elements... -->
  <img alt="Print screen image of things and stuff"
       loading="lazy"
       decoding="async"
       src="{{ 'path/to/image.jpeg' | absolute_url }}" />
</picture>
```
{% endraw %}


**Example HTML snip (after)**


{% raw %}
```html
<picture>
  <!-- ... Other source elements... -->
  <img alt="Print screen image of things and stuff"
       loading="lazy"
       decoding="async"
       width="800"
       height="600"
       src="{{ 'path/to/image.jpeg' | absolute_url }}" />
</picture>
```
{% endraw %}


Because this was a repetitive task I recorded a Vim macro similar to the following such that formatting was relatively quick...


```vim
0yi'k:read !./image-size.sh ^R0^MVk>...h^Vjx
```


**Macro Explanation**


- `0` moves the cursor to the first column

- `yi'` Yanks Inside single-quotes

- `k` moves the cursor up once

- `:` starts Ex mode

- `read !./image-size.sh` reads from a shell command via `!` prefix

- `^R0` puts the yanked file path within single-quotes

- `^M` is an escape-code for <kbd>Enter</kbd> within Ex mode

- `V` starts Visual selection, line mode

- `k` moves cursor to select current and previous line with Visual mode

- `>` indents visually selected lines

- `...` repeats last command three times

- `h` moves the cursor left once

- `^V` is an escape-code that starts Visual selection, block mode

- `j` moves cursor down once to select column of whitespace

- `x` deletes Visual selection


{% raw %}
After recording the above keystrokes, and using the macro once, I could then type <kbd>@</kbd><kbd>@</kbd> on each line beginning with _`src="{{ 'path/to/image.jpeg' | absolute_url }}"`_ to have width and height automatically inserted above that line.
{% endraw %}


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

