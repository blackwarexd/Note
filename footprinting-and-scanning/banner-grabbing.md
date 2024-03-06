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
    visible: false
---

# Banner grabbing

## Nmap

```bash
# Banner grabbing (NSE)
nmap -sV -O --script=banner $IP
```

## Netcat

```bash
nc -nv $IP $PORT
```
