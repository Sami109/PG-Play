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

Moving forward I started looking more into phpMyAdmin

![](attachments/Pasted%20image%2020250213205558.png)

I was able to login using the default credentials that were found on the tool "Creds Search". However, I have used the password "toor"

![](attachments/Pasted%20image%2020250213205822.png)