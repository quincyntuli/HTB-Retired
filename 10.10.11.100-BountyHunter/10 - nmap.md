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