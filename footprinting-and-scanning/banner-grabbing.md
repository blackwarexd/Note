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

# Banner grabbing

## Nmap

```bash
# Banner grabbing (NSE)
nmap -sV -O --script=banner $IP
```

## Netcat

```bash
nc -zv $IP $PORT
```
