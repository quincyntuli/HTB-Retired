# web
### https://seal.htb
![](seal.htb-01.png)
![](seal.htb-02.png)
![](seal.htb-03.png)

- site has nothing obviously discoverable
- found email address admin@seal.htb
- server is running nginx 1.18.0

<hr>

### http://seal.htb:8080
![](seal.htb-04.png)
- site allows for registration

![](seal.htb-05.png)
- There is information about how the server is configured. Tomcat is running behind Nginx configured as a  load balancer.

![](seal.htb-07.png)
- More information that relates to Tomcat
- The user interface is said to be disabled

![](seal.htb-09.png)
- Confirmation the interface is blocked.

![](seal.htb-08.gif)
- How the Tomcat referrence was discovered.

<hr>

### credential discovery

![](seal.htb-10.gif)
- The update feed reveals a series of file updates.
- tomcat-users.xml file is updated with some credentials
-  <span class="myYellow">username="tomcat"</span> <span class="myTurquoise">password="42MrHBf*z8{Z%"</span>
