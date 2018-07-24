### Description

Here are some useful scripts and exploits collected which can be used to escalate the privileges of the current user on a Linux system.
For credits check the appropriated source.

### Content
**[1] Information collecting**  
These scripts will collect several system information and print out the information useful for manual analysis. Collect them e.g. via `wget [ url ] --no-check-certificate`.
```
https://raw.githubusercontent.com/pentestmonkey/unix-privesc-check/1_x/unix-privesc-check
https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
https://raw.githubusercontent.com/mzet-/linux-exploit-suggester/master/linux-exploit-suggester.sh
http://www.securitysift.com/download/linuxprivchecker.py
```

**[2] Useful exploits**  
This is a collection of different exploits which might be handy for expanding privileges to root.   
Lookup kernel-version: `uname -r`
Dirtycow (<= 3.19.0 - 73.8)
```
https://gist.githubusercontent.com/rverton/e9d4ff65d703a9084e85fa9df083c679/raw/9b1b5053e72a58b40b28d6799cf7979c53480715/cowroot.c
```
Mempodipper (2.6.39 < 3.2.2)
```
https://www.exploit-db.com/raw/18411
```
RDS PE (<= 2.6.36-rc8)
```
https://www.exploit-db.com/raw/15285
```
KASLR/SMEP (4.4.0-83 < 4.8.0-58)
```
https://www.exploit-db.com/raw/43418/
```
Ubuntu 16.04.4 PE (< 4.4.0-116)
```
https://www.exploit-db.com/raw/44298/
```
ldso_dynamic Stack Clash (Debian 9/10, Ubuntu 14.04.5/16.04.2/17.04, Fedora 23/24/25)
```
https://www.exploit-db.com/raw/42276/
```
