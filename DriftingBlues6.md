
Initial scan

```
┌──(kali㉿kali)-[~/Desktop]
└─$ nmap 192.168.189.219    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-15 02:25 GMT
Nmap scan report for 192.168.189.219
Host is up (0.030s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.46 seconds
                                                                                                                              
┌──(kali㉿kali)-[~/Desktop]
└─$ nmap 192.168.189.219 -sV -sC 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-15 02:25 GMT
Nmap scan report for 192.168.189.219
Host is up (0.015s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.2.22 ((Debian))
|_http-title: driftingblues
| http-robots.txt: 1 disallowed entry 
|_/textpattern/textpattern
|_http-server-header: Apache/2.2.22 (Debian)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.98 seconds
```

Website main page

![](attachments/Pasted%20image%2020250214203819.png)

Web technologies

![](attachments/Pasted%20image%2020250214203840.png)

Robots.txt

![](attachments/Pasted%20image%2020250214203856.png)

	Login page / CMS

![](attachments/Pasted%20image%2020250214203929.png)

