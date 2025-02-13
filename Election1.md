```
┌──(kali㉿kali)-[~/Desktop]
└─$ nmap 192.168.233.211
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-14 01:59 GMT
Nmap scan report for 192.168.233.211
Host is up (0.016s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.42 seconds
                                                                                                                        
┌──(kali㉿kali)-[~/Desktop]
└─$ nmap 192.168.233.211 -p 22,80 -sV -sC
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-14 02:00 GMT
Nmap scan report for 192.168.233.211
Host is up (0.013s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 20:d1:ed:84:cc:68:a5:a7:86:f0:da:b8:92:3f:d9:67 (RSA)
|   256 78:89:b3:a2:75:12:76:92:2a:f9:8d:27:c1:08:a7:b9 (ECDSA)
|_  256 b8:f4:d6:61:cf:16:90:c5:07:18:99:b0:7c:70:fd:c0 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.09 seconds

```

**Robots.txt**

![](Pasted%20image%2020250213200510.png)

![[Pasted image 20250213195736.png]]

**Election Page**

![[Pasted image 20250213195828.png]]

