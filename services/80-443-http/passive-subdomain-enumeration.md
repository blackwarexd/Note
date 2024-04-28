---
description: >-
  Passive subdomain enumeration involves an adversary gathering subdomain
  information without directly interacting with the target.
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

# Passive Subdomain Enumeration

## VirusTotal

To receive information about a domain, type the domain name into the [<mark style="color:blue;">search bar</mark>](https://www.virustotal.com/gui/domain/) and click on the "**Relations**" tab.

## Certificates

Another interesting source of information we can use to extract subdomains is _<mark style="color:green;">**SSL/TLS**</mark>_ certificates. To discover additional domain names and subdomains for a target. We can use:

* [Censys.io](https://search.censys.io/certificates)
* [Crt.sh](https://crt.sh/)

```bash
# Query using Crt.sh and save the output
curl -s "https://crt.sh/?q=domain.com&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > output.txt

# OpenSSL
openssl s_client -ign_eof 2>/dev/null <<<$'HEAD / HTTP/1.0\r\n\r' -connect "domain.com:443" | openssl x509 -noout -text | grep 'DNS' | sed -e 's|DNS:|\n|g' -e 's|^\*.*||g' | tr -d ',' | sort -u
```

## TheHarvester

is a simple-to-use tools for gather information such as _<mark style="color:green;">**emails**</mark>_,_<mark style="color:green;">**names**</mark>_,_<mark style="color:green;">**subdomains**</mark>_,_<mark style="color:green;">**IP**</mark>_, and _<mark style="color:green;">**URLs**</mark>_ from various public sources.

```bash
# Create a "sources.txt" file, fills with modules for TheHarvester.
baidu
bufferoverun
crtsh
hackertarget
otx
projectdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye

# Execute theHarvester with "sources.txt" file created earlier.
cat sources.txt | while read source; do theHarvester -d "domain.com" -b $source -f "${source}-theHarvester"; done

# Extract all subdomains into a single file.
cat *.json | jq -r '.hosts[]' 2>/dev/null | cut -d':' -f1 | sort -u > subdomains-theHarvester.txt
```
