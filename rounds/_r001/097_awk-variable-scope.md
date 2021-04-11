---
layout: post
title: Awk Variable Scope
date: 2021-04-11 14:07:14 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Gotchas regarding Awk variable scoping
time_to_live: 1800

github:
  repo:
    url: https://github.com/S0AndS0/100-days-of-code/
    title: GitHub repository that builds this site

tweet:
  url: https://example.com
  title: Link to Tweet for this post
---



One of the gotchas that occasionally causes my Awk scripts to misbehave is the lack of `local`, or similar, keyword when defining variables. The closest solution I've found for preventing _scope-leak_ is defining extra function parameters.


Here's an example that demonstrates how variables declared within a function will be accessible outside of that block of code...


**`average.awk`**


```awk
#!/usr/bin/awk -f

{
  delete words_list[0]
  for (field_index = 1; field_index <= NF; field_index++) {
    words_list[field_index] = $field_index;
  }
  print "Avarage ->", average(words_list);
}

END {
  print "## Scope Leaked Variables ##"
  print "field_index ->", field_index;
  print "_sum        ->", _sum;
  print "_list_index ->", _list_index;
  print "_item       ->", _item;
}


function average(list) {
  _sum = 0;
  for (_list_index in list) {
    _item = list[_list_index];
    _sum += _item;
  }
  return _sum / length(list);
}
```


... And some example usage with output...


```bash
./average.awk <<EOF
1 2 3
4 5 6
6 7 8
EOF
#> Avarage -> 2
#> Avarage -> 5
#> Avarage -> 8
#> ## Scope Leaked Variables ##
#> field_index -> 4
#> _sum        -> 24
#> _list_index -> 3
#> _item       -> 9
```


While in above example this leakage may be harmless, where one to forget to reset the _`_sum`_ variable results would be inconsistent depending upon the number of lines read.


But as alluded to, there is a technique to mitigate possible issues, eg...


```awk
function average(list,
                 __sum__,
                 __index__,
                 __item__)
{
  for (__index__ in list) {
    __item__ = list[__index__];
    __sum__ += __item__;
  }
  return __sum__ / length(list);
}
```


... Function parameters are scoped to the code within that function!


> Note, the dunder (double underscore) syntax is **not** required but provides readers a _hint_ that such parameters do not need assigned at invocation.


______


## Contact and/or Contribute
[heading__contact_andor_contribute]: #contact-andor-contribute


For quick questions or suggestions you may reach out on [Twitter][link__twitter__s0_and_s0]. And to report mistakes, or provide corrections, please utilize [GitHub][link__github__s0ands0__100_days_of_code] to either open an Issue or Pull Request for this repository.



[link__github__s0ands0__100_days_of_code]: {{ page.github.repo.url }} "{{ page.github.repo.title }}"

[link__twitter__s0_and_s0]: {{ page.tweet.url }} "{{ page.tweet.title }}"

