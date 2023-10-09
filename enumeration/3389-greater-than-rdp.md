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

# 3389 -> RDP

## XfreeRDP

is an X11 _<mark style="color:green;">Remote Desktop Protocol</mark>_ (RDP) client which is part of the FreeRDP project.

```bash
# Connect with AUTHENTICATION
xfreerdp /u:Administrator /p:password123 /v:$IP:$PORT
```

## Hydra

is a brute force tool that is installed in Kali Linux by default. It can brute force the password/user's file list in several protocols.

```bash
hydra -l "Administrator" -P /wordlists/passwords.txt rdp://$IP -s $PORT
```

## MSFconsole

is a framework that holds many exploits, backdoors, scanners, etc. This is also known as _<mark style="color:green;">Metasploit</mark>_, by default, it is installed on Kali Linux.

```
# Checking RDP present, none default `port:3389`
auxiliary/scanner/rdp/rdp_scanner

# Enabling RDP
post/windows/manage/enable_rdp

# Scan OS, if it's vulnerable to bluekeep
auxiliary/scanner/cve_2019_0708_bluekeep

# Exploit the bluekeep (64 bit)
exploit/windows/rdp/cve_2019_0708_bluekeep_rce
```
