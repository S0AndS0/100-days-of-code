---
layout: post
title: Rust String Split Closure
date: 2021-01-10 17:10:06 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of string splitting with a callback closure
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    text: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1348440378849042433
  text: Link to Tweet for this post

attribution:
  links:
    - text: StackOverflow -- Convert a string to int?
      url: https://stackoverflow.com/questions/27043268/
      title: Convert a string to int?
      class: fa fa-stack-overflow

    - text: Rust -- Doc -- Closures
      url: https://doc.rust-lang.org/rust-by-example/fn/closures.html
      title: Rust documentation for closures
      class: fa fa-rust

    - text: Rust -- Doc -- Struct std::string::String
      url: https://doc.rust-lang.org/std/string/struct.String.html
      title: Rust documentation for String type data structures
      class: fa fa-rust
---



Unlike languages such as JavaScript that only accepts `char`, `String`, or `RegExp` types; the `String.split()` method in Rust is very powerful, because it can accept a callback closure/function too. For example it's possible to split a string on non-numerical characters...


```rust
fn main() {
    let v: Vec<&str> = "1.14.3".split(|c: char| !c.is_numeric()).collect();

    println!("v -> {:?}", v);
    assert_eq!(vec!["1", "14", "3"], v);
}
```


> Note, the closure should return Boolean for each character, because returning True/False determines if string is split at a given point.


By chaining with `.map()` the returned _chunks_ can be converted to another type too, eg...


```rust
fn main() {
    let n: Vec<i64> = "1.14.3".split(|c: char| !c.is_numeric())
                              .map(|c| c.parse::<i64>().unwrap())
                              .collect();

    println!("n -> {:?}", n);
    assert_eq!(vec![1, 14, 3], n);
}
```


---


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


---



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.text }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.text }}"

