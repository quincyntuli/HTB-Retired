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
