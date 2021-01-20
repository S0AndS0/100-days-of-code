---
layout: post
title: JavaScript Random UUID
date: 2021-01-19 22:02:00 -0800
#date_updated:  # Optional and formatted like 'date' above
description: Tips and example code for generating random UUIDs with JavaScript
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
    - text: StackOverflow -- How to create a GUID / UUID
      href: https://stackoverflow.com/questions/105034/
      title: How to create a GUID / UUID
      class: fa fa-stack-overflow

    - text: Wikipidea -- Universally unique identifier -- Version 4 (random)
      href: https://wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random)
      title: Universally unique identifier -- Version 4 (random)
      class: fa fa-wikipedia-w

    - text: 'Web Masters -- How do I open the JavaScript console in different browsers?'
      href: https://webmasters.stackexchange.com/questions/8525/
      title: How do I open the JavaScript console in different browsers?
      class: fa fa-stack-exchange
---



> Tips and example code for generating random UUIDs with JavaScript


---


- [UUID Function Source Code][heading__uuid_function_source_code]

- [Example Usage][heading__example_usage]

- [Explore With Browser Console][heading__explore_with_browser_console]

- [Attribution](#heading__attribution)


---


## UUID Function Source Code
[heading__uuid_function_source_code]: #uuid-function-source-code


Today I invested in writing a function for building UUID strings...


```javascript
/**
 * Returns Universally Unique ID compatible with version 4 (random)
 * @return {string}
 * @notes
 * - Format: xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx
 * @example
 * let uuid = UUID();
 * console.log(uuid);
 * //> a45054ba-d175-4aba-a75d-c74081e4da43
 * @author S0AndS0
 * @license AGPL-3.0
 */
function UUID() {
  // Int of low 32 bits of time
  const time_low = 'xxxxxxxx';

  // Int of middle 16 bits of time
  const time_mid = 'xxxx';

  // 4-bit "version" of most significatn bits followed by high 12 bits of time
  const time_hi_and_version = '4xxx';

  // 1 to 3 bit "variant" in most significant bits followed by 13 to 15 bit clock sequence
  const clock_seq_hi_and_res__clock_seq_low = 'yxxx';

  // 48 bit node ID
  const node_id = 'xxxxxxxxxxxx';

  return [
    time_low,
    time_mid,
    time_hi_and_version,
    clock_seq_hi_and_res__clock_seq_low,
    node_id,
  ].map((chunk) => {
    return chunk.replace(/[xy]/g, (c) => {
      const random = Math.random() * 16 | 0;
      if (c === 'x') {
        return random.toString(16);
      } else {
        return (random & 0x3 | 0x8).toString(16);
      }
    });
  }).join('-');
}
```


<script>
/**
 * Returns Universally Unique ID compatible with version 4 (random)
 * @return {string}
 * @notes
 * - Format: xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx
 * @example
 * let uuid = UUID();
 * console.log(uuid);
 * //> a45054ba-d175-4aba-a75d-c74081e4da43
 * @author S0AndS0
 * @license AGPL-3.0
 */
function UUID() {
  // Int of low 32 bits of time
  const time_low = 'xxxxxxxx';

  // Int of middle 16 bits of time
  const time_mid = 'xxxx';

  // 4-bit "version" of most significatn bits followed by high 12 bits of time
  const time_hi_and_version = '4xxx';

  // 1 to 3 bit "variant" in most significant bits followed by 13 to 15 bit clock sequence
  const clock_seq_hi_and_res__clock_seq_low = 'yxxx';

  // 48 bit node ID
  const node_id = 'xxxxxxxxxxxx';

  return [
    time_low,
    time_mid,
    time_hi_and_version,
    clock_seq_hi_and_res__clock_seq_low,
    node_id,
  ].map((chunk) => {
    return chunk.replace(/[xy]/g, (c) => {
      const random = Math.random() * 16 | 0;
      if (c === 'x') {
        return random.toString(16);
      } else {
        return (random & 0x3 | 0x8).toString(16);
      }
    });
  }).join('-');
}
</script>


______


## Example Usage
[heading__example_usage]: #example-usage


Here's an example of how to utilize the above function for storing client data...


```javascript
const clients = {};


function addClient(name, age, clients) {
  let uuid = UUID();
  while (clients.hasOwnProperty(uuid)) {
    uuid = UUID();
  }

  clients[uuid] = {
    name: String(name),
    age: Number(age),
  };
}


addClient('Bill', 23, clients);
addClient('Ted', 21, clients);


console.log(clients);
//> {
//>   '0d0015fd-272d-4c0c-8d6c-4870ee7d26ac': { name: 'Bill', age: 23 },
//>   'c152b112-f7ef-454f-b766-7c5ed9f681a8': { name: 'Ted', age: 21 }
//> }
```


______


## Explore With Browser Console
[heading__explore_with_browser_console]: #explore-with-browser-console


This page includes within it's source a copy of the above `function`, so readers that are utilizing a compatible web-browser may open the JavaScript console and experiment. Here's a quick list of browsers and the keyboard shortcuts that'll open the console...


- Chrome -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>K</kbd>

- Firefox -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>J</kbd>

- Opera -- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd>

- Safari -- <kbd>Cmd</kbd> + <kbd>Opt</kbd> + <kbd>c</kbd>


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.


______



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

