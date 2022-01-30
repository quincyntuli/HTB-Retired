# more UDP

## snmpwalk
- usually, one needs to download the MIB to translate the snmp addresses to human readable formats. 
````bash
sudo apt install snmp-mibs-downloader
````
- However, doing so might take away the ability to identify a missing `private address space` as arrived at through the following process

<HR>

- The private address space was arrived at after following a hint from DISCORD user 

![](PIT.HTB-01.png)

- after much googling and trial and error i came upon the perl script <span class="myYellowHighlight">snmpbw.pl</span> (is it bulkwalk ?)

## snmpbw.pl
- source https://github.com/dheiland-r7/snmp
	````bash
	./snmpbw.pl 10.10.10.241 public 2 1
	````
- The tool went further than the usual snmpwalk command
	````bash
	snmpwalk -v2c 10.10.10.241 -c public
	````
	![](PIT.HTB-02.png)
- This is the article where I learned about the idea of a `private node`
	https://blog.paessler.com/snmp-monitoring-via-oids-mibs

	![](PIT.HTB-03.png)
	
- After much expermimentation, snmpwalk can query the private node if it is specified.
	````bash
	snmpwalk -v2c 10.10.10.241 -c public 1.3.6.1.4
	````
	The result ...
	
	![](PIT.HTB-04.mp4)
	
	- from the result, a folder is discovered  <span id="seeddms" class="myYellowHighlight">/var/www/html/seeddms51x/seeddms
	</span>
 
	![](PIT.HTB-05.png)
	
	- from the result, a binary or  script (based on location <span class="myYellowHighlight">/usr/bin/</span> ) is found on <span class="myRedHighlight">/usr/bin/monitor</span>
	- the script or binary is <span class="myRedHighlight">red highlighted</span> because it turns out to be key to root.
	
	![](PIT.HTB-06.png)
	
	- further scrolling on the snmp result reveals possible usernames; 	root (duh) and <span class="myYellowHighlight">michelle</span>
	
	![](PIT.HTB-07.png)
	
	
	
	
	
	
	