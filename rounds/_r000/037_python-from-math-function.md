---
layout: post
title: Python from Math Function
date: 2020-06-03 10:48:41 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of translating Math function to Python syntax
time_to_live: 1800
mathjax: true
category: python
---



Math can be thought of as a domain specific programming language, and because it's been around for sometime, chances are good that there are solutions to common problems that can be translated computer programming languages.


Here's an example of a piecewise function written in Math notation...


$$
f(x) =
\begin{cases}
  \frac{x}{2}, & \text{if $x$ is even} \\[2ex]
  3n+1, &\text{if $x$ is odd}
\end{cases}
$$


... which be similar to a `switch`/`case` or `if`/`else` statement.


Here's an example of what the above notation could be written as using Python...


```python
def f(n):
  if n % 2 == 0:
    return n / 2
  else:
    return n * 3 + 1
```


Possibly the biggest difference between Math and other programming languages, aside from syntax, is that Math generally assumes computations to be interpreted in _meat-space_, where as computer programming languages are generally interpreted on chips.


## Attribution
[heading__attribution]: #attribution "Resources that where helpful in writing this post"


- [Math StackExchange (meta) -- Definitions by cases (piecewise functions)](https://math.meta.stackexchange.com/a/5025)
