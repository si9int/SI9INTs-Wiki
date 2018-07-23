### Description


This article how to access a restricted resource by defining a "X-Forwarded-For" header in the HTTP request.  
Credits to Shubham Sha, [source](https://shubs.io/enumerating-ips-in-x-forwarded-headers-to-bypass-403-restrictions/) and GingerLime

### Details

**[1] Bypassing 403**  
A server-side restriction of certain directories with a `.htaccess` using the following directive:
```
SetEnvIF X-FORWARDED-FOR [ ip ] AllowIP
e.g.: SetEnvIF X-FORWARDED-FOR "10.0.2.11" AllowIP
```
is useless and can be bypassed if a proxy lies between your request and the actual web-server. The required header is:
```
X-Forwarded-For: a, b, c, ...
a = client IP, b/c/.. = intermediate proxy (there is no limit to the number of proxies)
```
An application server must traverse the chain of proxies in reverse order to determine the most trustworthy IP address. By adding a large list of the same IP (which should match with the declaration) it is possible to access the limited resource.
```
GET /wp-admin/
X-Forwarded-For: 68.180.194.242, 68.180.194.242, 68.180.194.242, 68.180.194.242
```
[This tool](https://github.com/infosec-au/enumXFF) will automatically set the right header for a given IP range.
