---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Reverse shell upgrade

## Python

```bash
# This can be in either python3 or python2
python3 -c 'import pty;pty.spawn("/bin/bash")'
# Ctrl + Z [background]
stty raw -echo; fg [Return 2x]
export TERM=xterm
```

## Scripts

```bash
script /dev/null -c bash
# Ctrl + Z [background]
stty raw -echo; fg [Return 2x]
export TERM=xterm
```
