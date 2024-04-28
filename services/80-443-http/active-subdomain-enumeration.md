---
description: >-
  In active subdomain enumeration, an adversary gathers information by directly
  interacting with the target. This entails methods like port scanning,
  brute-forcing web applications, etc.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Active Subdomain Enumeration

## ZoneTransfer

The zone transfer is how a <mark style="color:green;">**secondary DNS server receives information from the primary DNS server and updates it**</mark>. There's web based [tool](https://hackertarget.com/zone-transfer/) that can performing the zone transfer automatically or doing it manually using _<mark style="color:green;">**nslookup**</mark>_.

```bash
# Identifying nameservers
nslookup -type=NS domain.com

# Performing the zone transfer
nslookup -type=any -query=AXFR domain.com ns.domain.com
```

## Gobuster

CLI tool that can use to perform subdomain enumeration.

```bash
# Using pattern to discover additional subdomains
# Save the pattern into a file - pattern.txt
i-want-this-pattern-{GOBUSTER}-ok

# Execute the gobuster with the given pattern
gobuster dns -r "ns.domain.com" -d "domain.com" -p pattern.txt -w wordlists.txt
```
