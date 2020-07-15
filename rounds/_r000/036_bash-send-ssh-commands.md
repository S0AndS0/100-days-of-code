---
layout: post
title: Bash send SSH commands
date: 2020-06-02 11:19:09 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using heredoc to send multiple commands to remote host
time_to_live: 1800
---



Example of using heredoc to send multiple commands to remote host...

```bash
ssh raspberrypi <<'EOF'
[[ -d "${PWD}/test-dir" ]] || {
  mkdir -vp "${PWD}/test-dir"
}

tee -a "${PWD}/test-dir/file.ext" 1>/dev/null <<EOL
user -> ${USER}
EOL
EOF
```

Note, `'EOF'` (with quotes) prevents parent shell from expanding variables and/or sub-shells, where as `EOL` (without quotes) allows the remote shell to expand things within that environment.
