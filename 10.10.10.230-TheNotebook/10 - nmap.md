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