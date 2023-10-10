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

# Port scanning

## Nmap

```bash
# All Port Scan
sudo nmap -p- --min-rate=10000 $IP
sudo nmap -p- --min-rate=10000 -oN nmap/allports $IP --open

# Script Port Scan
sudo nmap -p$PORT -sCV -oN nmap/output.txt $IP

# Script Vuln/Tag Port Scan
sudo nmap -p$PORT -sV --script=vuln -oN nmap/output.txt $IP

# Script port scan with exception
sudo nmap -sV --script "ldap* and not brute" -oN nmap/output.txt $IP

# UDP top100 ports
sudo nmap -sU -F $IP -oN output.txt

# Output XML to HTML
xsltproc output.xml -o output.html

# Grab all ports in output file
cat nmap/allports | grep "open" | grep -v "filtered" | cut -d "/" -f1 | sort -u | xargs | tr ' ' ',' > ports.txt
cat nmap/allports | grep "open" | grep -v "filtered" | cut -d "/" -f1 | sort -u | xargs | tr ' ' ',' | xclip -selection clipboard
```

## Netcat

```bash
# All TCP port scan
nc -zv $IP 01-65535

# All UDP port scan
nc -zv -u $IP 01-65535 
```
