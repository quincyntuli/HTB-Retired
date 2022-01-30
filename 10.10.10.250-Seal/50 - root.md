# root
````bash
sudo -l
````
- run sudo -l for any binaries that can be run without supplying password for user account

![](seal.htb-21.png)
- /usr/bin/ansible-playbook can be run without supplying password

![](seal.htb-22.png)
- According to GTFOBINS, the program is vulnerable

![](seal.htb-23.gif)
- running the command as suggested gets root.