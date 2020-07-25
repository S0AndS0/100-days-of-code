---
layout: post
title: Bash Command Redirection
date: 2020-05-20 09:41:55 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of passing commands to another account
time_to_live: 1800
category: bash
---



Example of passing commands to another account...


```bash
sudo su --shell /bin/bash --login "name" <<'EOF'
printf 'Home directory -> %s\n' "${HOME}"
EOF
```


Example of passing commands and outer variable/state to another account...


```bash
_outer_var="something"


sudo su --shell /bin/bash --login "name" <<EOF
printf 'Current directory -> %s\n' "\${PWD}"

(("${#_outer_var}")) || {
  exit 2
}

printf '_outer_var -> %s\n' "${_outer_var}"
EOF


printf "Exit code -> %i\n" "${?}"
```
