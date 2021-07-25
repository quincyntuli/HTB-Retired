# user
![](Armageddon-HTB-03.png)

- searchsploit suggests a specific Metasploit exploit

![](Armageddon-HTB-04.gif)

- Metasploit establishes a session

![](Armageddon-HTB-05.png)

- Stabilizing shell <span style="background-color:red;color:fff;font-weight:bold;">fails</span>

![](Armageddon-HTB-06.gif)


````php
$databases = array (
  'default' => 
  array (
    'default' => 
    array (
      'database' => 'drupal',
      'username' => 'drupaluser',
      'password' => 'CQHEy@9M*m23gBVj',
      'host' => 'localhost',
      'port' => '',
      'driver' => 'mysql',
      'prefix' => '',
    ),
  ),
);
````
- enumeration drupal site database connection settings reveals database credentials

![](Armageddon-HTB-07.gif)

- credentials were use to retrieve a hash
````
$S$DgL2gjv6ZtxBo6CdqZEyJuBphBmrCqIV6W97.oOsUf1xAhaadURt
````

![](Armageddon-HTB-08.gif)


````bash
john thehash --show
?:booboo

1 password hash cracked, 0 left
````

- the password matching the hash was in the wordilst *rockyou.txt* (````booboo````)

![](Armageddon-HTB-09.png)


- The only account on the machine that has access to an interactive shell is ``brucetherealadmin``

![](Armageddon-HTB-10.png)

- credendtials ````brucetherealadmin:booboo```` are able to login