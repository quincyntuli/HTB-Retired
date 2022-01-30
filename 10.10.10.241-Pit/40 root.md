# root
![](PIT.HTB-20.png)
- linpeas finds a writable folder at /usr/local/monitoring

![](PIT.HTB-21.png)
- this is confirmed when making a directory listing, the granularity is not common

![](PIT.HTB-06.png)
- recalling from UDP scan that there was a familiar reference to monitor or monitoring

![](PIT.HTB-22.png)
- the scripts suggets that a script placed on /usr/local/monitoring will be executed as long as it matches the wildcard check<span class="myTurquoise">\*</span>sh. (eg check<span class="myTurquoise">XYZ</span>.sh, check<span class="myTurquoise">ABC</span>.sh etc)

<hr>

### /usr/bin/monitor is limited

![](PIT.HTB-24.png)

![](PIT.HTB-23.png)

- the script is limited in that it is prevented from running any binaries such as nc.
- the script is not allowed to write files anywhere apart from authorized_keys
- this suggests generating a new public key and overwritting the current one to get root.

<hr>

### generating new public key

````bash
ssh-keygen
````

![](PIT.HTB-25.gif)

<hr>

### rooting

![](PIT.HTB-26.mp4)

- in a shell script checkABC.sh, the public key generated above is used to overwrite on the target /root/.ssh/authorized_keys 
- the corresponding private key is used to logon to the target as root.