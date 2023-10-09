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

# 22 - SSH

## Netcat

```bash
# Banner grabbing
nc $IP 22
```

## Nmap Scripts

```bash
# Enum authentication methods
sudo nmap -p22 --script=ssh-auth-methods --script-args="ssh.user=root" $IP

# Enum algorithm used
sudo nmap -p22 --script=ssh2-enum-algos $IP

# Enum hostkey server's fingerprint
sudo nmap -p22 --script=ssh-hostkey --script-ags ssh_hostkey=full $IP

# Bruteforcing
sudo nmap -p22 --script=ssh-brute --script-args userdb=/wordlists/users.txt $IP
```

## Hydra

```bash
hydra -l "root" -P /wordlists/passwords.txt $IP ssh
```

## MSFconsole

```bash
auxiliary/scanner/ssh/ssh_version
auxiliary/scanner/ssh/ssh_login
auxiliary/scanner/ssh/ssh_enumusers

# Check if SSH vulnerable to AUTHENTICATION bypass
auxiliary/scanner/ssh/libssh_auth_bypass
```
