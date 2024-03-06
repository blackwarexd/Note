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

# 53 - DNS

## Dig

```bash
# DNS zone / email
dig soa example.com

# Nameserver
dig ns example.com

# DNS server version
dig CH TXT version.bind $IP

# All the records
dig any example.com @$IP

# Zone transfer
dig axfr example.com @$IP

# Bash oneliner subdomain bruteforce
for sub in $(cat /wordlists/subdomains.txt);do dig $sub.example.com @$IP | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done
```

## DNSrecon

```bash
# Enumerate general DNS records for a given domain such as MX,SOA,NS,A, etc
dnsrecon -d example.com
```

## DNSenum

```bash
# Subdomain bruteforce
dnsenum --dnsserver $IP --enum -p 0 -s 0 -o subdomains.txt -f /wordlists/subdomains.txt example.com
```
