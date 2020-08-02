---
layout: post
title: Rust implement custom addition
date: 2020-08-02 16:29:08 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of implementing math for custom data structure
time_to_live: 1800
---



Example of implementing math for custom data structure...


```rust
struct Eggs {
  count: u32
}

impl Eggs {
  fn new(count: u32) -> Self {
    Self { count }
  }
}


impl ops::Add<Eggs> for Eggs {
  type Output = Eggs;

  fn add(self, other: Self) -> Self {
    Self { count: self.count + other.count }
  }
}
```


Usage example...


```rust
let egg_one = Eggs::new(1);
let egg_two = Eggs::new(2);
let eggs = egg_one + egg_two;
println!("eggs.count -> {}", eggs.count);
//> eggs.count -> 3
```
