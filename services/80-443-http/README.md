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

# 80,443 - HTTP

```fsharp
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  ssl/https
```

```bash
nc -v domain.com 80
openssl s_client -connect domain.com:443
```

## Infrastructure Identification

A web application's infrastructure is what keeps it running and allows it to function. Web servers are directly involved in any web application's operation. Some of the most popular are Apache, Nginx and Microsoft IIS, among others.

{% content-ref url="passive-infrastructure-identification.md" %}
[passive-infrastructure-identification.md](passive-infrastructure-identification.md)
{% endcontent-ref %}

{% content-ref url="active-infrastructure-identification.md" %}
[active-infrastructure-identification.md](active-infrastructure-identification.md)
{% endcontent-ref %}

## Subdomain Enumeration

Subdomain enumeration refers to mapping all available subdomains within a domain name. It increases the attack surface and may uncover hidden management backend panels or intranet web applications.

{% content-ref url="passive-subdomain-enumeration.md" %}
[passive-subdomain-enumeration.md](passive-subdomain-enumeration.md)
{% endcontent-ref %}

{% content-ref url="active-subdomain-enumeration.md" %}
[active-subdomain-enumeration.md](active-subdomain-enumeration.md)
{% endcontent-ref %}

## Crawling

Crawling a website is the _<mark style="color:green;">**systematic**</mark>_ or _<mark style="color:green;">**automatic**</mark>_ process of exploring a website to list of the resources encountered along the way. We use the crawling process to find as many _<mark style="color:green;">**pages**</mark>_ and _<mark style="color:green;">**subdirectories**</mark>_ belonging to a website as possible.

### <mark style="color:green;">Ffuf</mark>

```bash
# Ffuf recursively
ffuf -u http://domain.com/FUZZ -w /wordlists.txt -recursion -recursion-depth 1

# Ffuf directories,files,extensions
ffuf -w directories.txt:DIRECTORY,wordlists.txt:WORDLIST,extensions.txt:EXTENSIONS -u http://domain.com/DIRECTORY/WORDLISTEXTENSIONS
```

## Virtual Hosts

A virtual host (vHost) is a feature that allows several websites to be hosted on a single server. There are two ways to configure virtual hosts:

* <mark style="color:green;">**IP**</mark>-based virtual hosting
* <mark style="color:green;">**Name**</mark>-based virtual hosting

### <mark style="color:green;">IP-based virtual hosting</mark>

A host can have multiple network interfaces. Multiple IP addresses, or interface aliases, can be configured on each network of a host.

### <mark style="color:green;">Name-based virtual hosting</mark>

The distinction for which domain the service was requested is made at the application level. For example, several domain names, such as admin.domain.com and dev.domain.com, can refer to the same IP.

```bash
# Sending curl request with the host header
curl -s http://domain.com -H "Host: vhost.domain.com"

# vHost fuzzing using curl
cat vhosts.txt | while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********"; curl -s -I http://domain.com -H "HOST: ${vhost}.domain.com" | grep "Content-Length: "; done

# Ffuf vhost
ffuf -u http://domain.com -H "Host: FUZZ.domain.com" -w wordlists.txt -fs 500
```

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>General</td><td></td><td><a href="general.md">general.md</a></td></tr><tr><td>WebDAV</td><td></td><td><a href="webdav.md">webdav.md</a></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>
