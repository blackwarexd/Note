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

# WebDAV

## Nmap Scripts

```bash
# Enum webdav type
sudo nmap -p80 --script=http-webdav-scan --script-args http-methods.url-path=/webdav/ $IP

# Enum webdav supported methods
sudo nmap -p80 --script=http-methods --script-args http-methods.url-path=/webdav/ $IP
```

## DAVtest

```bash
# Without authentication
davtest -url http://$IP/webdav
davtest -url http://$IP

# With authentication
davtest -auth administrator:password123 -url http://$IP/webdav
davtest -auth administrator:password123 -url http://$IP
```

## CaDAVer

```bash
# Connect to webdav
cadaver http://$IP/webdav
# prompt username:
# prompt password:
```

## Hydra

```bash
hydra -L /wordlists/username.txt -P /wordlists/password.txt $IP http-get /webdav/
```

## MSFconsole

```bash
exploit/windows/iis/iis_webdav_upload_asp
```
