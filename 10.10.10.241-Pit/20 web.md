# 20 web

## 10.10.10.241
![](PIT.HTB-08.png)
- the is a reference that points towards the file system where ngix root folder is located <span class="myYellow">/usr/share/nginx/html<span>

<hr>
	

## PIT.HTB
![](PIT.HTB-09.png)
- The vhost <span class="myTurquoise" style="font-weight: bold;">PIT.HTB</span> loads the same page with  a reference that points towards the file system where ngix root folder is located <span class="myYellow">/usr/share/nginx/html<span>

<hr>

	
## 10.10.10.241:9090
![](PIT.HTB-10.png)
- no creds available to login here.

<hr>

## PIT.HTB:9090
![](PIT.HTB-11.png)
- no creds available to login here.

<hr>

	
## dms-pit.htb
- nmap had reveald the vhost <span class="myTurquoise">dms-pit.htb</span>

<div class="myprediv">
|    
| ssl-cert: Subject: commonName=<span class="myTurquoise">dms-pit.htb</span>/organizationName=4cd9329523184b0ea52ba0d20a1a6f92/countryName=US
| Subject Alternative Name: DNS:<span class="myTurquoise">dms-pit.htb</span>, DNS:localhost, IP Address:127.0.0.1
| Issuer: commonName=<span class="myTurquoise">dms-pit.htb</span>/organizationName=4cd9329523184b0ea52ba0d20a1a6f92/countryName=US/organizationalUnitName=ca-5763051739999573755
| Public Key type: rsa
</div>
	 
	

![](PIT.HTB-12.png)
- nothing hosted on the root
	
<hr>

### Searching for URL that is hosting  <span class="myYellowHighlight">/var/www/html/seeddms51x/seeddms</span>

- This location was discovered from the UDP scan [[12  more UDP#snmpbw pl]]
	
To search : -

- http://10.10.10.241/seeddms51x/seeddms
- http://pit.htb/seeddms51x/seeddms
- http://10.10.10.241:9090/seeddms51x/seeddms
- http://pit.htb:9090/seeddms51x/seeddms
- http://dms-pit.htb/seeddms51x/seeddms

![](PIT.HTB-13.png)

- The first 4 did not render and page

![](PIT.HTB-14.gif)
	
- The fifth one renders a site

