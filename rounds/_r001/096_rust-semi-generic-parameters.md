---
layout: post
title: Rust Semi-Generic Parameters
date: 2021-04-10 16:59:31 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Using `where` keyword to define Generic type behavior
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
    - text: Barely Functional -- How do I convert a &str to a String in Rust?
      href: https://blog.mgattozzi.dev/how-do-i-str-string/
      title: How do I convert a &str to a String in Rust?
      class: nil
---



Much of my early experience with programming languages involved those that didn't have type definitions. Python, prior to version `3.<something>`, for example is considered _duck-typed_ meaning that if an object "quacks like a duck, it is a duck". Rust in most cases however, requires that types are well defined; either explicitly or inferred.


Or so I thought!


As it turns out there is a way to define generic types via `where` keyword that describes the behavior of a parameter or variable. For example the following function may accept either `&str` or `String` for the _`file_path`_ parameter...


```rust
fn first_line_of_file<S>(file_path: S) -> Result<String>
    where
        S: Into<String>
{
    let p = file_path.into();
    let f = File::open(p)?;

    let reader = BufReader::new(f);
    let mut lines = reader.lines();

    return lines.next().unwrap();
}
```


... in fact any kind of data that implements `.into()` that returns a `String` type is acceptable to the `first_line_of_file` function!


Additionally it be possible to define a generic that implements traits such as addition...


```rust
fn adder<T>(left: T, right: T) -> T
    where
        T: std::ops::Add<Output = T>
{
    return left + right;
}
```


... the above `adder` function is able to add any number types, well so long as both _`left`_ and _`right`_ parameters where of the same type.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

