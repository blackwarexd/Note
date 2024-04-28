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

# Passive Infrastructure Identification

## Netcraft

[It](https://sitereport.netcraft.com/) offer us information about the servers without even interacting with them.

## Wayback Machine

A library of free public access to digitalized materials, including websites, collected automatically via its web crawlers. This [tool](http://web.archive.org/) can be used to _<mark style="color:green;">**find older versions**</mark>_ of a website at a point in time.

Another tool called [waybackurls](https://github.com/tomnomnom/waybackurls) is a command-line utility used to inspect URLs saved by Wayback Machine and look for specific keywords.

```bash
# Crawled URLs from a domain with the date.
waybackurls -dates http://domain.com > waybackurls.txt
```
