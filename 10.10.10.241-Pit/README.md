# nmap

## TCP Scan
<div class="myprediv">
# Nmap 7.91 scan initiated Sat Jun 12 21:43:59 2021 as: nmap -sC -sC -A -p- -vv --open -oA nmap/10.10.10.241-Pit 10.10.10.241
Nmap scan report for 10.10.10.241
Host is up, received syn-ack (0.62s latency).
Scanned at 2021-06-12 21:44:00 SAST for 2004s
Not shown: 65532 filtered ports
Reason: 63742 no-responses and 1790 host-unreaches
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT     STATE SERVICE         REASON  VERSION
<span class="myYellow">22/tcp   open  ssh             syn-ack OpenSSH 8.0 (protocol 2.0)</span>
| ssh-hostkey: 
|   3072 6f:c3:40:8f:69:50:69:5a:57:d7:9c:4e:7b:1b:94:96 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDPRtC3Zd+DPBo1Raur/oVw/vz3BFbDkm6wmyb+E+0kBcgsDzm+UZqGn3u+rbI9L7PtNCIOTHa4j0Qs6fD9CvWa9xl1PXPQEI4X8UIfiDKduW+NhC0tRtfKzBSIR0XE+n2MjNCLM6pAR4xwhPZcpkXQmwurayT3OOHPV5QpOdSfzp0Zv56sBn3FmYe9j6fuhRFFL2x6Q8NfHOFkd4tAwkcCB1EebD0S/1ajB+TO6WeMOIHEU9HAAyg2LDzUKh0pzfFdK2MQHzKrGcFe3kOalz/dRJApa9wzUgq6iDbQvstDucPFLmvu8Y4YKFg1trKnf4Z2kopSUn0kKOxBROddoKOBdTyE309PF1b/Jo4ziDVVkRvPIHh06Se7NRVzbRtO8mBTFbi/Efag8QtLHeLDnF5SJj5SdTBiMiLvyGNWs3UySweOazyijw5bQtlgKbZHy0tLsjOCWjTuXGHAS3pHkkgSYKfr/NwWDsVQwHgCf1M7EZ23Uxww/qE6vRWbHStc6gM=
|   256 c2:6f:f8:ab:a1:20:83:d1:60:ab:cf:63:2d:c8:65:b7 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBASBJvHyFZwgmAuf2qWsMHborC5pS152XK8TVyTESkcPGWHqVAa/9rmFNvMuiMvBTPWhPq2+b5apFURHdxW2S5Q=
|   256 6b:65:6c:a6:92:e5:cc:76:17:5a:2f:9a:e7:50:c3:50 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJmDbvdFwHALNAnJDXuRD6aO9yppoVnKbTLbUmn6CWUn
<span class="myYellow">80/tcp   open  http            syn-ack nginx 1.14.1</span>
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-server-header: nginx/1.14.1
|_http-title: Test Page for the Nginx HTTP Server on Red Hat Enterprise Linux
<span class="myYellow">9090/tcp open  ssl/zeus-admin? syn-ack</span>
| fingerprint-strings: 
|   GetRequest, HTTPOptions: 
|     HTTP/1.1 400 Bad request
|     Content-Type: text/html; charset=utf8
|     Transfer-Encoding: chunked
|     X-DNS-Prefetch-Control: off
|     Referrer-Policy: no-referrer
|     X-Content-Type-Options: nosniff
|     Cross-Origin-Resource-Policy: same-origin
|    
| ssl-cert: Subject: commonName=<span class="myTurquoise">dms-pit.htb</span>/organizationName=4cd9329523184b0ea52ba0d20a1a6f92/countryName=US
| Subject Alternative Name: DNS:<span class="myTurquoise">dms-pit.htb</span>, DNS:localhost, IP Address:127.0.0.1
| Issuer: commonName=<span class="myTurquoise">dms-pit.htb</span>/organizationName=4cd9329523184b0ea52ba0d20a1a6f92/countryName=US/organizationalUnitName=ca-5763051739999573755
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-04-16T23:29:12
| Not valid after:  2030-06-04T16:09:12
| MD5:   0146 4fba 4de8 5bef 0331 e57e 41b4 a8ae
| SHA-1: 29f2 edc3 7ae9 0c25 2a9d 3feb 3d90 bde6 dfd3 eee5
| -----BEGIN CERTIFICATE-----
| MIIEpjCCAo6gAwIBAgIISl2h4yex5dEwDQYJKoZIhvcNAQELBQAwbzELMAkGA1UE
| BhMCVVMxKTAnBgNVBAoMIDRjZDkzMjk1MjMxODRiMGVhNTJiYTBkMjBhMWE2Zjky
| MR8wHQYDVQQLDBZjYS01NzYzMDUxNzM5OTk5NTczNzU1MRQwEgYDVQQDDAtkbXMt
| cGl0Lmh0YjAeFw0yMDA0MTYyMzI5MTJaFw0zMDA2MDQxNjA5MTJaME4xCzAJBgNV
| BAYTAlVTMSkwJwYDVQQKDCA0Y2Q5MzI5NTIzMTg0YjBlYTUyYmEwZDIwYTFhNmY5
| MjEUMBIGA1UEAwwLZG1zLXBpdC5odGIwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAw
| ggEKAoIBAQDZLaNRUf3BXYCd+Df9XZwMBmIwGzy/yX+9fPY6zGXYEYS7SeH9xZ7p
| GTUQMfk30Olb7rzftCKx9xSMHyoCJIAWFeVDV9vxJbGaEqFRvKHPeqcpQbRAKoqL
| xWaqbDZCXsBtTVYEwpRHvJ/GoGEWAQSbP1zkHzvVBkHuXE7Sj0zlW5NaBjvG/wEe
| wAB6crwnIYoqC550cMPritvjLwijk9nhwaPJ462anhJR5vFBvkR4nqD3mhIytUOb
| YMsfVoI0FiXtlBdu1ApABxtIdQgkY94eRAaMTkQ4Je0a8G5PlRZ20xCdqHb3xIZV
| 1mphZehkUeN0MzgEloL5TX8Zab+LZW+ZAgMBAAGjZzBlMA4GA1UdDwEB/wQEAwIF
| oDAJBgNVHRMEAjAAMCcGA1UdEQQgMB6CC2Rtcy1waXQuaHRigglsb2NhbGhvc3SH
| BH8AAAEwHwYDVR0jBBgwFoAUc8ssOet8O2a3+F2If4eQixSV7PwwDQYJKoZIhvcN
| AQELBQADggIBAG8kou51q78wdzxiPejMv9qhWlBWW3Ly5TvAav07ATx8haldEHvT
| LlFNGPDFAvJvcKguiHnGrEL9Im5GDuzi31V4fE5xjzWJdkepXasK7NzIciC0IwgP
| 7G1j11OUJOt9pmDRu2FkTHsSdr5b57P4uXS8rRF5lLCEafuemk6ORXa07b9xSrhC
| 3pWl22RtVlTFQ3wX8OsY0O3w5UUz8T/ezhKYUoM/mYQu+ICTAltlX4xae6PGauCh
| uaOY+/dPtM17KfHSbnCS1ZnR0oQ4BXJuYNfOR/C59L5B7TWzaOx5n1TD6JHOzrDu
| LxjO0OTeFaBRXL/s2Z5zNPTpZVnHyKEmHr5ZObjR6drDGqXfShPq5y70RfE28Pxm
| VTCdK4MCqDkELIlXrxzHQ/IPC8pxho6WEQsY80xZ1nXbLshlymh6clgblOetToZT
| HObIkEoPBtszUssFmWSN5hd4JcuyqSbJhichYtFQRASb2I4jWdP831LPir+MCGQv
| iAnieBF8zYus7kboTwfXmBGUt6r6eNE1yr4ZXPxOZoWq2ob6aAeLp2mqif+jgUSk
| fiG9oiAoyXWxw5pLfYHxVQGY+rGbjOs8gCAxBaTPt6dCkHZy/nU8PNZtV6QC4OME
| LI/sYtmG8XENdQhsLM2sewOMvv5rgsZ8SlX05Bw8C1xuq5Rg1KewCjlY
|_-----END CERTIFICATE-----
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jun 12 22:17:24 2021 -- 1 IP address (1 host up) scanned in 2004.28 seconds
</div>



## UDP Scan

````bash
# Nmap 7.91 scan initiated Wed Jun 23 22:43:47 2021 as: nmap -sU --top-ports 100 -oA nmap/10.10.10.241-UDP-top-100-rescan 10.10.10.241
Nmap scan report for pit.htb (10.10.10.241)
Host is up (0.25s latency).
Not shown: 99 filtered ports
PORT    STATE         SERVICE
161/udp open|filtered snmp

# Nmap done at Wed Jun 23 22:45:33 2021 -- 1 IP address (1 host up) scanned in 106.60 seconds
````
- Open UDP port confirmed, this warrants further enumeration ([[12  more UDP]])

# more UDP

## snmpwalk
- usually, one needs to download the MIB to translate the snmp addresses to human readable formats. 
````bash
sudo apt install snmp-mibs-downloader
````
- However, doing so might take away the ability to identify a missing `private address space` as arrived at through the following process

<HR>

- The private address space was arrived at after following a hint from DISCORD user 

![](PIT.HTB-01.png)

- after much googling and trial and error i came upon the perl script <span class="myYellowHighlight">snmpbw.pl</span> (is it bulkwalk ?)

## snmpbw.pl
- source https://github.com/dheiland-r7/snmp
	````bash
	./snmpbw.pl 10.10.10.241 public 2 1
	````
- The tool went further than the usual snmpwalk command
	````bash
	snmpwalk -v2c 10.10.10.241 -c public
	````
	![](PIT.HTB-02.png)
- This is the article where I learned about the idea of a `private node`
	https://blog.paessler.com/snmp-monitoring-via-oids-mibs

	![](PIT.HTB-03.png)
	
- After much expermimentation, snmpwalk can query the private node if it is specified.
	````bash
	snmpwalk -v2c 10.10.10.241 -c public 1.3.6.1.4
	````
	The result ...
	
	![](PIT.HTB-04.mp4)
	
	- from the result, a folder is discovered  <span id="seeddms" class="myYellowHighlight">/var/www/html/seeddms51x/seeddms
	</span>
 
	![](PIT.HTB-05.png)
	
	- from the result, a binary or  script (based on location <span class="myYellowHighlight">/usr/bin/</span> ) is found on <span class="myRedHighlight">/usr/bin/monitor</span>
	- the script or binary is <span class="myRedHighlight">red highlighted</span> because it turns out to be key to root.
	
	![](PIT.HTB-06.png)
	
	- further scrolling on the snmp result reveals possible usernames; 	root (duh) and <span class="myYellowHighlight">michelle</span>
	
	![](PIT.HTB-07.png)
	
	
	
	
	
	# more UDP

## snmpwalk
- usually, one needs to download the MIB to translate the snmp addresses to human readable formats. 
````bash
sudo apt install snmp-mibs-downloader
````
- However, doing so might take away the ability to identify a missing `private address space` as arrived at through the following process

<HR>

- The private address space was arrived at after following a hint from DISCORD user 

![](PIT.HTB-01.png)

- after much googling and trial and error i came upon the perl script <span class="myYellowHighlight">snmpbw.pl</span> (is it bulkwalk ?)

## snmpbw.pl
- source https://github.com/dheiland-r7/snmp
	````bash
	./snmpbw.pl 10.10.10.241 public 2 1
	````
- The tool went further than the usual snmpwalk command
	````bash
	snmpwalk -v2c 10.10.10.241 -c public
	````
	![](PIT.HTB-02.png)
- This is the article where I learned about the idea of a `private node`
	https://blog.paessler.com/snmp-monitoring-via-oids-mibs

	![](PIT.HTB-03.png)
	
- After much expermimentation, snmpwalk can query the private node if it is specified.
	````bash
	snmpwalk -v2c 10.10.10.241 -c public 1.3.6.1.4
	````
	The result ...
	
	![](PIT.HTB-04.mp4)
	
	- from the result, a folder is discovered  <span id="seeddms" class="myYellowHighlight">/var/www/html/seeddms51x/seeddms
	</span>
 
	![](PIT.HTB-05.png)
	
	- from the result, a binary or  script (based on location <span class="myYellowHighlight">/usr/bin/</span> ) is found on <span class="myRedHighlight">/usr/bin/monitor</span>
	- the script or binary is <span class="myRedHighlight">red highlighted</span> because it turns out to be key to root.
	
	![](PIT.HTB-06.png)
	
	- further scrolling on the snmp result reveals possible usernames; 	root (duh) and <span class="myYellowHighlight">michelle</span>
	
	![](PIT.HTB-07.png)
	
	
	
	
	
	
	# User

![](PIT.HTB-15.png)

- Guessed credentials michelle:michelle log on successfully
- A note suggests it is upgraded from 5.1.10 to 5.1.15


<HR>

## exploit

![](PIT.HTB-16.png)

- there is an RCE by Ninit Jain ( https://www.linkedin.com/in/nimitiitk/ ) for version 5.1.11 , however according to the note, the current version is 5.1.15
- chancing the exploit in the hope that it would still work ...
- link to exploit https://www.exploit-db.com/exploits/47022


### trying the exploit
	

![](PIT.HTB-17.mp4)
	
- Trying the exploit works
	
<HR>

### enumetating for more credentials

![](PIT.HTB-18.mp4)

- credentials found <span class="myYellow"> dbUser="seeddms" |  dbPass=<span style="font-weight:bold;">"ied^ieY6xoquu"</span> </span>

<HR>

### logging on to CentOS Linux Cock<span class="myTurquoise">pit</span>

![](PIT.HTB-19.mp4)
	
- working credentials for user are <span class="myYellow"> dbUser=<span style="font-weight:bold;">"michelle"</span> |  dbPass=<span style="font-weight:bold;">"ied^ieY6xoquu"</span> </span>


	
	
	
	# root
![](PIT.HTB-20.png)
- linpeas finds a writable folder at /usr/local/monitoring

![](PIT.HTB-21.png)
- this is confirmed when making a directory listing, the granularity is not common

![](PIT.HTB-06.png)
- recalling from UDP scan that there was a familiar reference to monitor or monitoring

![](PIT.HTB-22.png)
- the scripts suggets that a script placed on /usr/local/monitoring will be executed as long as it matches the wildcard check<span class="myTurquoise">\*</span>sh. (eg check<span class="myTurquoise">XYZ</span>.sh, check<span class="myTurquoise">ABC</span>.sh etc)

<hr>

### /usr/bin/monitor is limited

![](PIT.HTB-24.png)

![](PIT.HTB-23.png)

- the script is limited in that it is prevented from running any binaries such as nc.
- the script is not allowed to write files anywhere apart from authorized_keys
- this suggests generating a new public key and overwritting the current one to get root.

<hr>

### generating new public key

````bash
ssh-keygen
````

![](PIT.HTB-25.gif)

<hr>

### rooting

![](PIT.HTB-26.mp4)

- in a shell script checkABC.sh, the public key generated above is used to overwrite on the target /root/.ssh/authorized_keys 
- the corresponding private key is used to logon to the target as root.
	