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

# 21 - FTP

## Nmap Scripts

```bash
# Enum FTP with all NSE
nmap -p21 --script=ftp-* $IP

# Perform brute-force
nmap -p21 --script=ftp-brute --script-agrs userdb=/wordlists/users.txt $IP
```

## Banner Grabbing

```bash
nc -nv $IP 21
openssl s_client -connect $IP:21 -starttls ftp
```

## FTP tools

```bash
ftp $IP
>anonymous        # Username
>anonymous        # Password
> status          # Show current status
> ls -a           # List hidden files
> ls -R           # Recursively listing files
> get file.txt    # Download a file (file.txt)
> put file.txt    # Upload a file (file.txt)
> exit            # Exit 
```

## Download all files

```bash
# Download recursively
wget -m ftp://'anonymous:anonymous'@$IP

# Download recursively
wget -m --no-passive ftp://'anonymous:anonymous'@$IP
```

## Hydra

```bash
hydra -L /wordlists/users.txt -P /wordlists/passwords.txt $IP ftp
```

## MSFconsole

```bash
service postgresql start

auxiliary/scanner/ftp/ftp_version          # ftp version enumeration
auxiliary/scanner/ftp/anonymous            # check for anonymous login
auxiliary/scanner/ftp/ftp_login            # ftp brute-force

# vsftpd v2.3.4
exploit/unix/ftp/vsftpd_234_backdoor
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
