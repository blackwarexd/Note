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

# Active Infrastructure Identification

## HTTP Headers

Identify the webserver version based on response headers. There are also _<mark style="color:green;">**other characteristics**</mark>_ to take into account while fingerprinting _<mark style="color:green;">**web servers in the response headers**</mark>_. Such as, `X-Powered-By` header or `Cookies`.

Some of the default cookie values are:

* <mark style="color:green;">**.NET**</mark> : `ASPSESSIONID<RANDOM>=<COOKIE_VALUE>`
* <mark style="color:green;">**PHP**</mark> : `PHPSESSID=<COOKIE_VALUE>`
* <mark style="color:green;">**JAVA**</mark> : `JSESSION=<COOKIE_VALUE>`

```bash
# View the response headers
curl -I http://$IP
```

## WhatWeb

Command-line tools for analyze _<mark style="color:green;">**web technologies**</mark>_, _<mark style="color:green;">**CMS**</mark>_, _<mark style="color:green;">**blogging platforms**</mark>_, _<mark style="color:green;">**packages used**</mark>_, _<mark style="color:green;">**JavaScript libraries**</mark>_ and many more.

```bash
# Default scanning
whatweb http://$IP -v

# Aggressively scan the target
whatweb -a3 http://$IP -v

# Scan based on list
whatweb -i hostnames.txt -a3 -v
```

## Wappalyzer

It's a browser [extension](https://www.wappalyzer.com/) that has similar functionality to WhatWeb, but the results are displayed while navigating the target URL.

## WafW00f

A web application firewall (_<mark style="color:green;">**WAF**</mark>_) fingerprinting tool that send requests and analyses responses to determine if a security solution is in place.

```bash
# Check all possible WAFs used.
wafw00f -a http://$IP -v

# Check all possible WAFs (target list)
wafw00f -i hostnames.txt -a -v
```

## Aquatone

An automatic and visual inspection [tool](https://github.com/michenriksen/aquatone) for quickly gaining an overview of _<mark style="color:green;">**HTTP-based attack surfaces**</mark>_ by scanning a list of configurable ports, visiting the website, and taking a screenshot.

This is helpful, especially when dealing with _<mark style="color:green;">**huge subdomain lists**</mark>_.

```bash
# Installation
sudo apt install chromium-driver
go install -v github.com/michenriksen/aquatone@latest

# Execute the aquatone
cat subdomains.txt | aquatone -out ./aquatone -screenshot-timeout 1000
```
