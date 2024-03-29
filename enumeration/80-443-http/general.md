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

# General

## Nmap Scripts

```bash
# Enum HTTP
sudo nmap -p80 --script=http-enum $IP

# Enum headers in index page
sudo nmap -p80 --script=http-headers $IP

# Enum HTTP banner
sudo nmap -p80 --script=banner $IP

# Enum HTTP methods
sudo nmap -p80 --script=http-methods $IP
```

## General Enumeration

```bash
# Listing the HTTP headers
curl -s -I http://$IP

# Listing the HTTP headers
# sudo apt install httpie in [debian/ubuntu](based)
http $IP

# Checking all vulnerability
whatweb $IP
```

## Directory Enumeration

```bash
# gobuster command
gobuster dir -u http://$IP -w /wordlists/directory.txt

# ffuf command
ffuf -u http://$IP/FUZZ -w /wordlists/directory.txt

# dirb command
dirb http://$IP /wordlists/directory.txt
```

## Subdomain Enumeration

```bash
# gobuster DNS
gobuster dns -d example.com -w /wordlists/directory.txt

# gobuster VHOST
gobuster vhost -u example.com -w /wordlists/directory.txt

# ffuf VHOST
ffuf -u http://example.com -H "Host: FUZZ.example.com" -w /wordlists/directory.txt
```

## MSFconsole

```bash
auxiliary/scanner/http/brute_dirs
auxiliary/scanner/http/http_version            # enumerate version
auxiliary/scanner/http/http_header             # enumerate web server header
auxiliary/scanner/http/robots_txt              # enumerate robots.txt
auxiliary/scanner/http/dir_scanner             # directories brute-force
auxiliary/scanner/http/apache_userdir_enum     # enumerate user (apache)
auxiliary/scanner/http/http_login              # http login brute-force

auxiliary/scanner/http/files_dir     # files brute-force (like ffuf -recursive)
exploit/windows/http/rejetto_hfs_exec          # rejetto hfs2.3
exploit/multi/http/tomcat_jsp_upload_bypass    # Apache
```

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>General</td><td></td><td><a href="./">.</a></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>
