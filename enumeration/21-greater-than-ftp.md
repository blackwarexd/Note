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

# 21 -> FTP

## Nmap Scripts

The example command for enumerating _<mark style="color:green;">File Transfer Protocol</mark>_ (FTP) with Nmap is here.

```bash
# Enum FTP with all NSE
nmap -p21 --script=ftp-* $IP

# Perform brute-force
nmap -p21 --script=ftp-brute --script-agrs userdb=/wordlists/users.txt $IP
```

## General Enumeration

```bash
# View SSL on FTP
openssl s_client -connect $IP:$PORT -starttls ftp

# View Config file
cat /etc/vsftpd.conf | grep -v "#"

# List users can't access to FTP
cat /etc/ftpusers
```

## FTP tools (anonymous)

is a command line utility/tool that is installed by default in Kali Linux. It can be used to log into a _<mark style="color:green;">File Transfer Protocol</mark>_ (FTP) server and download/upload files.

```bash
ftp $IP
# prompt user: anonymous
# prompt password: anonymous or NULL
```

## Hydra

is a brute force tool that is installed in Kali Linux by default. It can brute force the password/user's file list in several protocols.

```bash
hydra -L /wordlists/users.txt -P /wordlists/passwords.txt $IP ftp
```

## MSFconsole

is a framework that holds many exploits, backdoors, scanners, etc. This is also known as _<mark style="color:green;">Metasploit</mark>_, by default, it is installed on Kali Linux.

```bash
service postgresql start

auxiliary/scanner/ftp/ftp_version          # ftp version enumeration
auxiliary/scanner/ftp/anonymous            # check for anonymous login
auxiliary/scanner/ftp/ftp_login            # ftp brute-force

# vsftpd v2.3.4
exploit/unix/ftp/vsftpd_234_backdoor
```
