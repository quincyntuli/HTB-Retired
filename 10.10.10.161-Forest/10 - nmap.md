# nmap

## initial scan

````bash
$ nmap -p- -vv --open -oA nmap/10.10.10.161-Forest 10.10.10.161
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-07 16:09 SAST
Initiating Ping Scan at 16:09
Scanning 10.10.10.161 [2 ports]
Completed Ping Scan at 16:09, 0.24s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 16:09
Completed Parallel DNS resolution of 1 host. at 16:09, 0.01s elapsed
Initiating Connect Scan at 16:09
Scanning 10.10.10.161 [65535 ports]
Discovered open port 135/tcp on 10.10.10.161
Discovered open port 445/tcp on 10.10.10.161
Discovered open port 139/tcp on 10.10.10.161
Discovered open port 53/tcp on 10.10.10.161
Connect Scan Timing: About 18.56% done; ETC: 16:11 (0:02:16 remaining)
Discovered open port 88/tcp on 10.10.10.161
Discovered open port 593/tcp on 10.10.10.161
Discovered open port 49671/tcp on 10.10.10.161
Discovered open port 49665/tcp on 10.10.10.161
Connect Scan Timing: About 28.69% done; ETC: 16:12 (0:02:32 remaining)
Connect Scan Timing: About 29.20% done; ETC: 16:14 (0:03:41 remaining)
Connect Scan Timing: About 29.73% done; ETC: 16:15 (0:04:46 remaining)
Connect Scan Timing: About 30.26% done; ETC: 16:17 (0:05:48 remaining)
Connect Scan Timing: About 30.71% done; ETC: 16:18 (0:06:48 remaining)
Discovered open port 49676/tcp on 10.10.10.161
Connect Scan Timing: About 30.09% done; ETC: 16:20 (0:08:10 remaining)
Connect Scan Timing: About 30.43% done; ETC: 16:22 (0:09:11 remaining)
Connect Scan Timing: About 30.70% done; ETC: 16:23 (0:10:12 remaining)
Connect Scan Timing: About 31.07% done; ETC: 16:25 (0:11:08 remaining)
Connect Scan Timing: About 31.43% done; ETC: 16:26 (0:12:02 remaining)
Connect Scan Timing: About 31.74% done; ETC: 16:28 (0:12:56 remaining)
Connect Scan Timing: About 32.17% done; ETC: 16:29 (0:13:57 remaining)
Connect Scan Timing: About 37.03% done; ETC: 16:29 (0:12:52 remaining)
Discovered open port 5985/tcp on 10.10.10.161
Discovered open port 49684/tcp on 10.10.10.161
Connect Scan Timing: About 59.17% done; ETC: 16:22 (0:05:34 remaining)
Discovered open port 3268/tcp on 10.10.10.161
Discovered open port 47001/tcp on 10.10.10.161
Discovered open port 49706/tcp on 10.10.10.161
Discovered open port 49666/tcp on 10.10.10.161
Discovered open port 3269/tcp on 10.10.10.161
Discovered open port 389/tcp on 10.10.10.161
Connect Scan Timing: About 79.26% done; ETC: 16:19 (0:02:15 remaining)
Discovered open port 636/tcp on 10.10.10.161
Discovered open port 49677/tcp on 10.10.10.161
Discovered open port 9389/tcp on 10.10.10.161
Discovered open port 49664/tcp on 10.10.10.161
Discovered open port 464/tcp on 10.10.10.161
Completed Connect Scan at 16:18, 564.44s elapsed (65535 total ports)
Nmap scan report for 10.10.10.161
Host is up, received conn-refused (0.24s latency).
Scanned at 2021-07-07 16:09:06 SAST for 565s
Not shown: 64714 closed ports, 799 filtered ports
Reason: 64714 conn-refused and 799 no-responses
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT      STATE SERVICE          REASON
53/tcp    open  domain           syn-ack
88/tcp    open  kerberos-sec     syn-ack
135/tcp   open  msrpc            syn-ack
139/tcp   open  netbios-ssn      syn-ack
389/tcp   open  ldap             syn-ack
445/tcp   open  microsoft-ds     syn-ack
464/tcp   open  kpasswd5         syn-ack
593/tcp   open  http-rpc-epmap   syn-ack
636/tcp   open  ldapssl          syn-ack
3268/tcp  open  globalcatLDAP    syn-ack
3269/tcp  open  globalcatLDAPssl syn-ack
5985/tcp  open  wsman            syn-ack
9389/tcp  open  adws             syn-ack
47001/tcp open  winrm            syn-ack
49664/tcp open  unknown          syn-ack
49665/tcp open  unknown          syn-ack
49666/tcp open  unknown          syn-ack
49671/tcp open  unknown          syn-ack
49676/tcp open  unknown          syn-ack
49677/tcp open  unknown          syn-ack
49684/tcp open  unknown          syn-ack
49706/tcp open  unknown          syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 564.75 seconds
````


## second scan

<div class="myprediv" >
nmap -sC -sV -p 53,88,135,139,389,445,464,593,636,3268,3269,5985,9389,47001,49664,49665,49666,49671,49676,49677,49684,49706 -oA nmap/10.10.10.161-Forest-second 10.10.10.161
PORT      STATE SERVICE      VERSION
<span class="myYellow">53/tcp    open</span> domain Simple DNS Plus
<span class="myYellow">88/tcp    open</span> kerberos-sec Microsoft Windows Kerberos (server time: 2021-07-07 15:14:24Z)
<span class="myYellow">135/tcp   open  msrpc </span> Microsoft Windows RPC
<span class="myYellow">139/tcp   open  netbios-ssn</span> Microsoft Windows netbios-ssn
389/tcp   open  ldap Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
<span class="myYellow">445/tcp   open</span>  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap Microsoft Windows Active Directory LDAP (Domain: <span class="myTurquoise" style="font-weight:bold;">htb.local</span>, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
<span class="myYellow">5985/tcp  open</span> http Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf       .NET Message Framing
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49671/tcp open  msrpc        Microsoft Windows RPC
49676/tcp open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
49677/tcp open  msrpc        Microsoft Windows RPC
49684/tcp open  msrpc        Microsoft Windows RPC
49706/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows
<pre>
Host script results:
|_clock-skew: mean: 2h29m58s, deviation: 4h02m30s, median: 9m58s
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST
|   NetBIOS computer name: FOREST\x00
|   Domain name: htb.local
|   Forest name: htb.local
|   FQDN: FOREST.htb.local
|_  System time: 2021-07-07T08:15:17-07:00
| smb-security-mode: 
|   account_used: \<blank\>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-07-07T15:15:20
|_  start_date: 2021-07-06T19:15:28
</pre>
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 80.49 seconds

</div>