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


