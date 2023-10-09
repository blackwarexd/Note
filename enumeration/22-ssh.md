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

# 22 -> SSH

## Netcat

is a networking utility for reading from and writing to network connections using TCP/IP.

```bash
# Banner grabbing
nc $IP 22
```

## Nmap Scripts

The example command for enumerating _<mark style="color:green;">Secure Shell</mark>_ (SSH) with Nmap is here.

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

is a brute force tool that is installed in Kali Linux by default. It can brute force the password/user's file list in several protocols.

```bash
hydra -l "root" -P /wordlists/passwords.txt $IP ssh
```

## MSFconsole

is a framework that holds many exploits, backdoors, scanners, etc. This is also known as _<mark style="color:green;">Metasploit</mark>_, by default, it is installed on Kali Linux.

```bash
auxiliary/scanner/ssh/ssh_version
auxiliary/scanner/ssh/ssh_login
auxiliary/scanner/ssh/ssh_enumusers

# Check if SSH vulnerable to AUTHENTICATION bypass
auxiliary/scanner/ssh/libssh_auth_bypass
```
