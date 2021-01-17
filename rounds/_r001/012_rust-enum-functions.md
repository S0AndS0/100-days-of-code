---
layout: post
title: Rust Enum Functions
date: 2021-01-16 20:20:04 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Example of adding introspection functions to `enum` types
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    text: GitHub repository that builds this site

tweet:
  url: https://twitter.com/S0_And_S0/status/1350665547642503168
  text: Link to Tweet for this post
---



One of the things I'm growing to like about the Rust language is that even `enum` types can be enhanced with _`impl`mentation_ functions. For example here's an `enum` that describes the `Day` type and an `impl` that adds introspection functions...


```rust
#[allow(dead_code)]

enum Day {
    Monday,
    Tuesday,
    Wednsday,
    Thursday,
    Friday,
    Saturday,
    Sunday
}


impl Day {
    fn is_weekday(&self) -> bool {
        match self {
            &Self::Saturday | &Self::Sunday => { false },
            _ => { true }
        }
    }

    fn is_weekend(&self) -> bool {
        !self.is_weekday()
    }
}


fn main() {
    let friday = Day::Friday;
    let saturday = Day::Saturday;
    let sunday = Day::Sunday;
    println!("friday.is_weekday() -> {}", friday.is_weekday());
    println!("saturday.is_weekday() -> {}", saturday.is_weekday());
    println!("sunday.is_weekend() -> {}", sunday.is_weekend());
}
```


... This greatly simplifies _down-stream_ code because common _`match`-able_ logic can be abstracted.


---


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


---



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.text }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.text }}"

