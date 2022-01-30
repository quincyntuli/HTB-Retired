# nmap
<div class="myprediv">
# Nmap 7.91 scan initiated Sun Jun 27 20:03:35 2021 as: nmap -sC -sV -A -vv --open -p- -oA nmap/10.10.10.244-Dynstr 10.10.10.244
Nmap scan report for 10.10.10.244
Host is up, received syn-ack (0.23s latency).
Scanned at 2021-06-27 20:03:35 SAST for 98s
Not shown: 64563 closed ports, 969 filtered ports
Reason: 64563 conn-refused and 969 no-responses
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE REASON  VERSION
<span class="myYellow">22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)</span>
<pre>
| ssh-hostkey: 
|   3072 05:7c:5e:b1:83:f9:4f:ae:2f:08:e1:33:ff:f5:83:9e (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC//sbOTQwLRH4CGj3riDnnTvTCiJT1Uz7CyRSD2Tkh2wkT20rtAq13c5M1LC2kxki2bz9Ptxxx340Cc9tAcQaPZbmHndQe/H1bGiVZCKjOl2WqWQTV9fq6GGtflC94BkkLrmkWHzqg+S50g2Zg0iesPMkKAmwqwEVZx9npe1QuF3RQu5EYQXRYVOzpqQdU+jRD267gCvsKp9xmr7trZ1UzFxfBUOzSCWa3Adm2TTFwiA5jTb6x0lKVnQtgKghioMQeXXPuiTLCbI0XfbksoRI2OBAvTZf7RsIthKCiyCQRWjVh5Idr5Fh7GgwYaDgW662W3V3hCNEQRY8R9/fXWdVho1gWbm6NFt+NyRO/6F2XDvPseBYr+Yi6zwGEM+PpsTi5dfj8yYKRZ3HFXwjeBGjCPMRe9XPpCvvDnHAF18B1INVJPSwAIVll365V5D18JslQh7PpAWxO70TzmEC9E+UPXOrt29tZ0Zi/uApFRM700pdOhnvcs8q4RBWaUpp3ZB0=
|   256 3f:73:b4:95:72:ca:5e:33:f6:8a:8f:46:cf:43:35:b9 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBFtYzp8umMbm7o9+1LUTVio/dduowE/AsA3rO52A5Q/Cuct9GY6IZEvPE+/XpEiNCPMSl991kjHT+WaAunmTbT4=
|   256 cc:0a:41:b7:a1:9a:43:da:1b:68:f5:2a:f8:2a:75:2c (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOz8b9MDlSPP5QJgSHy6fpG98bdKCgvqhuu07v5NFkdx
</pre>
<span class="myTangerine">53/tcp open  domain  syn-ack ISC BIND 9.16.1 (Ubuntu Linux)</span>
| dns-nsid: 
|_  bind.version: 9.16.1-Ubuntu
<span class="myYellow">80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))</span>
<pre>
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Dyna DNS
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Jun 27 20:05:13 2021 -- 1 IP address (1 host up) scanned in 98.28 seconds
</pre>
</div>

## ports to be investigated
- port 22 - always the least most interesting 
- port 53 - not very commong on HTB. This is the most interesting vector considering the name 
- port 80 - mandatory visit

