---
layout: post
title: Rust Reading Files
date: 2021-04-07 16:52:50 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Some examples of reading lines, and characters from files via Rust
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  URL: https://twitter.com/S0_And_S0/status/1379951875374583816
  title: Link to Tweet for this post
---



I've been mulling over an idea for a special type of file parser for a while, today I invested some time into learning how I may accomplish this long-term goal, and thought it'd be useful for others if I shared how such projects begin.


Before writing any code it is a good idea to initialize a new Rust project via the `cargo` command...


```bash
cargo init --lib ~/git/local/rust-examples/file_parser
```


... then change the current working directory to the new project path...


```bash
cd ~/git/local/rust-examples/file_parser
```


---


Now be the time to write some source code to experiment with...


**`src/lib.rs`**


```rust
#!/usr/bin/env rust


use std::io::prelude::*;
use std::io::BufReader;
use std::io::Result;
use std::fs::File;


pub fn file_line_reader(file_path: &str) -> Result<String> {
    let f = File::open(file_path)?;
    let mut reader = BufReader::new(f);

    let mut line = String::new();
    reader.read_line(&mut line)?;
    return Ok(line);
}


pub fn file_char_reader(file_path: &str) -> String {
    let f = File::open(file_path).unwrap();
    let reader = BufReader::new(f);

    reader.lines()
          .next()
          .unwrap()
          .unwrap()
          .chars()
          .next()
          .unwrap()
          .to_string()
}


#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_file_line_reader() {
        let first_line = file_line_reader("test-file.txt").unwrap();
        assert_eq!(first_line, "First Line!\n");
    }

    #[test]
    fn test_file_char_reader() {
        let fist_char = file_char_reader("test-file.txt");
        assert_eq!(fist_char, "F");
    }
}
```


**Notes**


- within the `file_line_reader` function the `?` of lines `let f = File::open(file_path)?;`, and `reader.read_line(&mut line)?;`, is short-hand for unwrapping that works for functions that return an Option or Result type

- within the `file_char_reader` function the _mess_ of `.next()`, `.unwrap()`, etc. calls for `reader` is currently the shortest method I've found for reading the first character of a file; suggestions are very welcomed in regards to more eloquent/efficient parsing techniques


---


For completeness the content of test file may be similar to...


```
First Line!
Second Line?
```


---


Run tests via `cargo` command...


```bash
cargo test
```


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

