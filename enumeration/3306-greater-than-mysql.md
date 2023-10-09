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

# 3306 -> MySQL

## Nmap Scripts

The example command for enumerating _<mark style="color:green;">MySQL</mark>_ with Nmap is here.

```bash
# Enum version/info/capabilities/attribute MySQ
sudo nmap -p3306 --script=mysql-info $IP

# Enum empty password/anonymous login
sudo nmap -p3306 --script=mysql-empty-password $IP

# Enum MySQL audit with AUTHENTICATION
sudo nmap -p3306 --script=mysql-audit --script-args "mysql-audit.username='root',mysql-audit.password='password123',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'" $IP

# Enum users with AUTHENTICATION
sudo nmap -p3306 --script=mysql-users --script-args "mysqluser='root',mysqlpass='password123'" $IP

# Enum databases with AUTHENTICATION
sudo nmap -p3306 --script=mysql-databases --script-args "mysqluser='root',mysqlpass='password123'" $IP

# Enum all variables with AUTHENTICATION
sudo nmap -p3306 --script=mysql-variables --script-args "mysqluser='root',mysqlpass='password123'" $IP

# Dump hashes with AUTHENTICATION
sudo nmap -p3306 --script=mysql-dump-hashes --script-args "username='root',password='password123'" $IP

# Query database with AUTHENTICATION
sudo nmap -p3306 --script=mysql-query --script-args "query='select count(*) from books.authors;',username='root',password='password123'" $IP
```

## MySQL tool

is a command line utility to interact/log into databases in _<mark style="color:green;">MySQL</mark>. Check_ [_this_](https://book.hacktricks.xyz/network-services-pentesting/pentesting-mysql#mysql-commands) _for more commands._

```bash
# Login to MySQL (password prompt)
mysql -h $IP -u root
    [none]> show databases;
    [none]> use <database>;
    [database]> show tables;
    [database]> show columns from <table>;
    [database]> select * from <table>;
    [database]> select load_file("/etc/passwd");
```

## Hydra

is a brute force tool that is installed in Kali Linux by default. It can brute force the password/user's file list in several protocols.

```bash
hydra -l "root" -P /wordlists/passwords.txt $IP mysql
```

## MSFconsole

is a framework that holds many exploits, backdoors, scanners, etc. This is also known as _<mark style="color:green;">Metasploit</mark>_, by default, it is installed on Kali Linux.

```bash
auxiliary/scanner/mysql/mysql_version
auxiliary/scanner/mysql/mysql_schemadump
auxiliary/scanner/mysql/mysql_writeable_dirs
auxiliary/scanner/mysql/mysql_file_enum #check readable files
auxiliary/scanner/mysql/mysql_hashdump
auxiliary/scanner/mysql/mysql_login

# Require AUTHENTICATION
auxiliary/admin/mysql/mysql_enum
auxiliary/admin/mysql/mysql_sql
```
