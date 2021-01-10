---
layout: post
title: Rust Application Module
date: 2021-01-09 20:19:18 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Quick guide for organizing and using modules within a Rust application
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    text: GitHub repository that builds this site

tweet:
  url: https://example.com
  text: Link to Tweet for this post
---



As with nearly all other projects, creating a Git repository is a good idea for tracking file changes...


```bash
git init application-name

cd application-name
```


---


Rust has a package/dependency manager, check `cargo --help` for a full list of options, at this point the `init` command is useful for initializing _scaffolding_ for a new project...


```bash
cargo init
```


---


Modules are a shared resource for a project and may be within files, or organized under sub-directories; generally I find using sub-directories easier to expand upon in the future...


```bash
mkdir src/name_space

touch src/name_space/mod.rs
```


> Note, for those that prefer a file based approach, the above could be instead organized as...
>
> `touch src/name_space.rs`
>
> ... and nothing else about this guide _should_ require alteration.


---


Example source files...


**`src/name_space/mod.rs`**


```rust
pub mod module_name {
    //! Private function may be called within same scope
    fn private_function() {
        println!("Called `module_name::private_function()`");
    }

    //! Public function may be called from other processes
    pub fn public_function() {
        println!("Called `module_name::public_function()`");
    }

    //! Access private_function() with a public function
    pub fn indirect_access() {
        println!("Called `module_name::indirect_access()`");
        private_function();
    }
}
```


**`src/main.rs`**


```rust
mod name_space;
use name_space::module_name;


fn main() {
    module_name::public_function();
    module_name::indirect_access();
}
```


---



The `cargo` command has a convenient option for compiling and running an application...


```bash
cargo run
```


... which _should_ output something similar to...


```
Called `module_name::public_function()`
Called `module_name::indirect_access()`
Called `module_name::private_function()`
```


---


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.




[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.text }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.text }}"

