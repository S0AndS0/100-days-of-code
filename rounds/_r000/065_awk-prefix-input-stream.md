---
layout: post
title: Awk prefix input stream
date: 2020-07-01 14:09:03 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Script that conditionally prefixes input stream
time_to_live: 1800
---



Awk script that conditionally prefixes input stream only if there is input...


**`prefix-stream.awk`**


```awk
#!/usr/bin/awk -f


BEGIN {
  if (!header) { exit 1; }
  getline _line
  if (!length(_line)) { exit; }
  print header
  print _line
}

{ print; }
```


## Usage examples


Piped input...


```bash
echo 'something' | prefix-stream.awk -v header='---\nprefix\n---'
```


Here doc input...


```bash
prefix-stream.awk -v header='---\nprefix\n---' <<'EOF'
something
EOF
```


Example output for either of above...


```
---
prefix
---
something
```


Multiple files input...


```bash
tee -a one.txt 1>/dev/null <<'EOF'
another thing
EOF


tee -a two.txt 1>/dev/null <<'EOF'
something else
EOF


prefix-stream.awk -v header='---\nprefix\n---' one.txt two.txt
```


Example output...


```
---
prefix
---
another thing
something else
```
