# ffuf
└─$ ffuf -w /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt -u http://love.htb/FUZZ

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.3.1 Kali Exclusive <3
________________________________________________

 :: Method           : GET
<span class="myYellowHighlight"> :: URL              : http://love.htb/FUZZ</span>
 :: Wordlist         : FUZZ: /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

includes                [Status: 301, Size: 332, Words: 22, Lines: 10]
plugins                 [Status: 301, Size: 331, Words: 22, Lines: 10]
<span class="myYellowHighlight">admin</span>                   [Status: 301, Size: 329, Words: 22, Lines: 10]
images                  [Status: 301, Size: 330, Words: 22, Lines: 10]
Admin                   [Status: 301, Size: 329, Words: 22, Lines: 10]
webalizer               [Status: 403, Size: 298, Words: 22, Lines: 10]
Images                  [Status: 301, Size: 330, Words: 22, Lines: 10]
phpmyadmin              [Status: 403, Size: 298, Words: 22, Lines: 10]
Includes                [Status: 301, Size: 332, Words: 22, Lines: 10]
ADMIN                   [Status: 301, Size: 329, Words: 22, Lines: 10]
dist                    [Status: 301, Size: 328, Words: 22, Lines: 10]
IMAGES                  [Status: 301, Size: 330, Words: 22, Lines: 10]
tcpdf                   [Status: 301, Size: 329, Words: 22, Lines: 10]
licenses                [Status: 403, Size: 417, Words: 37, Lines: 12]
server-status           [Status: 403, Size: 417, Words: 37, Lines: 12]
                        [Status: 200, Size: 4388, Words: 654, Lines: 126]
PlugIns                 [Status: 301, Size: 331, Words: 22, Lines: 10]
INCLUDES                [Status: 301, Size: 332, Words: 22, Lines: 10]
Plugins                 [Status: 301, Size: 331, Words: 22, Lines: 10]
con                     [Status: 403, Size: 298, Words: 22, Lines: 10]
aux                     [Status: 403, Size: 298, Words: 22, Lines: 10]
prn                     [Status: 403, Size: 298, Words: 22, Lines: 10]
server-info             [Status: 403, Size: 417, Words: 37, Lines: 12]
:: Progress: [30000/30000] :: Job [1/1] :: 167 req/sec :: Duration: [0:03:00] :: Errors: 2 ::
