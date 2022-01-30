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
