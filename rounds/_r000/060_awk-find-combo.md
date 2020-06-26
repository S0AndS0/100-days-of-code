---
layout: post
title: Awk Find combo
date: 2020-06-26 14:24:03 -0700
#date_updated:  # Optional and formatted like Fri Jun 26 14:24:03 PDT 2020 above
description: Example of combining `awk` and `find` command-line utilities
time_to_live: 1800
---



Example of combining `awk` and `find` command-line utilities...


```bash
find . -type f | xargs awk -v pattern='#_message' '{
  if ($0 ~ pattern) {
    print FILENAME ":", FNR, "->", $0
  }
}'
```


Example output...


```
./x11vnc-push-xwindow/x11vnc-push-xwindow : 96 ->     # if (("${#_message}")); then
./x11vnc-push-xwindow/x11vnc-push-xwindow : 99 ->     (("${#_message}")) && {
```


Generalized Awk script...


**`awk-find.awk`**


```awk
#!/usr/bin/awk -f

BEGIN {
  directory = directory? directory: "."
  if (!pattern) {
    print "No search pattern defined!"
    exit 1
  }

  cmd = "find " directory " -type f"
  while ( (cmd | getline file) > 0) {

    while ( (getline line < file) > 0 ) {
      line_no++
      if (line ~ pattern) {
        print file, ":", line_no, "->", line
      }
    }
    line_no = 0
    close(file)

  }
  close(cmd)
}
```


Example usage for `awk-find.awk` script...


```bash
./awk-find.awk directory='.' pattern='#_message'
```


___


## Attribution
[heading__attribution]: #attribution "&#x1F4C7; Resources that where helpful in writing this post so far."


- [GNU Awk -- 4.10.4 Using `getline` into a Variable from a File](https://www.gnu.org/software/gawk/manual/html_node/Getline_002fVariable_002fFile.html)
