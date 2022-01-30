# web

## fuzzing for files

````bash
ffuf -w /opt/SecLists/Discovery/Web-Content/raft-medium-files.txt -u http://bountyhunter.htb/FUZZ -fs 281
````

![](BountyHunter.HTB-06.png)
- These notes are made after the fact.
- This means the above fuzzing command is one I arrived at to give the prettiest outlook for the screenshot.
- The results yield two files of interest; <span class="myTurquoise"><b>portal.php</b></span> and <span class="myTangerine"><b>db.php</b></span>

<hr>

## link to <span class="myTurquoise">portal.php</span>

![](BountyHunter.HTB-01.png)
- on the landing page, there is a link to portal.php

<hr>

## link to log_submit.php
![](BountyHunter.HTB-02.png)
- on portal.php there is a link to log_submit.php

<hr>

## log_submit.php
![](BountyHunter.HTB-03.png)
- log_submit.php has a form that merely takes form input and merely throws it back on the screen using javascript DOM.

![](BountyHunter.HTB-04.png)

- One can see on Burp how log_submit.php submitting form input to tracker_diRbPr00f314.php
- Form data seems base64 formatted.

![](BountyHunter.HTB-05.png)

````xml
<?xml  version="1.0" encoding="ISO-8859-1"?>
		<bugreport>
		<title>qdadaTitle</title>
		<cwe>qdadaCWE</cwe>
		<cvss>qdadaCVSS Score</cvss>
		<reward>$29.99</reward>
		</bugreport>
````
- one can see how the base64 formatted data is actually and XML data exchange.
- this brings to mind an XXE vulnerability