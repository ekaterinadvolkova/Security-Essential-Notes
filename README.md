# Security Essential Notes

## Penetration testing
### Enumeration (learn the state of the target)
* Check connection: ````ping```` {target_IP}
* Scan ports with name of identified services: ````sudo nmap -sV```` {target_IP}

### Foothold (check if accounts have blank passwords)
* Typical account names: ````admin````, ````administrator````, ````root````

#### Telnet
* Runs on port ````23```` TCP by default,
* ````telnet```` {target_IP}
* ````ls````
* ````get```` filename

#### File Transfer Protocol (FTP)
* To check if ftp is properly installed ````sudo apt install ftp -y````
* To see available ftp services: ````ftp -h````
* Check target ftp: ````ftp```` {target_IP}, try login
* ````ls```` to see available files, ````get```` filename, ````bye```` to quit ````ftp```` mode
* ````get```` filename
* ````cat```` filename

#### Server Message Block (SMB)
* Shared access to files, printers, serial ports between endpoint on network
* Ususally port ````445```` is open for SMB
* To enumerate share content ````snbclient```` is used
* ````sudo apt-get install smbclient````
* To see available sharenames ````smbclient -L```` {target_IP}
* To get to the available share where files are stored: ````smbclient \\\\ {target_IP} \\ {target_SHARE}````

#### REmote DIctionary Server (REDIS)
* Open-source advanced NoSQL key-value data store used as a database, cache, and message broker
* Scan network with ports, and version detection: ````sudo nmap -p- -sV```` {target_IP}
* Install redis CLI: ````sudo apt install redis-tools````
* To get help: ````redis cli --help````
* Get hostname: ````redis-cli -h```` {target_IP}
* To get more information about the host: ````info```
* ````Keyspace```` section provides statistics on the main dictionary of each database
* List all keys: ````keys *````

#### Secure Shell Protocol (SSH)
* Runs on port ````23```` by default

#### CLI - Remote Access Tools
* RDP (Remote Desktop Protocol) operates on ports ````3389```` TCP and ````3389```` UDP
* To install ````xfreerdp````: ````sudo apt-get install freerdp2-x11````
* To specify the target IP for connection: ````xfreerdp /v:```` {target_IP}
* ````/cert:ignore```` : Specifies to the scrips that all security certificate usage should be
ignored.
* ````/u:Administrator```` : Specifies the login username to be "Administrator".
* ````/v:{target_IP}```` : Specifies the target IP of the host we would like to connect to.


### SQL
* Install/ update: ````sudo apt update && sudo apt install mysql*````
* ````sudo nmap -sV -sC ```` {target_IP} to scan open for the database
* ````sudo apt-get install mariadb-server````
* ````mysql -u root -p -h ```` {target_IP}
* ````SHOW DATABASES;```` - show databases
* ````SHOW FULL TABLES FROM htb;````
* ````SHOW COLUMNS FROM config FROM htb;````
* ````USE htb;```` - to connect to certain DB
*  ````SHOW tables;```` - to show tables inside the DB
*  ````SELECT * FROM config;````
*  ````root```` can be used without password


### SQL-Injections
* ````Gobuster````, ````Dirbuster````, ````Dirb```` are tools for brute-forcing (enumerating hidden directories)
* Install ````go```` environment: ````go install github.com/OJ/gobuster/v3@latest````
* Install ````gobuster````: 
    * ````go install github.com/OJ/gobuster/v3@latest````
    * ````git clone https://github.com/OJ/gobuster.git````
    * ````go get && go build````
    * ````go install````

### MongoDB
* Install the ````mongodb```` utility on Debian-based Linux distributions: 
  * ````curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.4.7.tgz````
* Extract the contents of the ````tar```` archive file using the tar utility:
  * ````tar xvf mongodb-linux-x86_64-3.4.7.tgz````
* Navigate to the location where the ````mongo```` binary is present
  * ````cd mongodb-linux-x86_64-3.4.7/bin````
* Connect to the MongoDB server running on the remote host as an anonymous user
  * ````./mongo mongodb://{target_IP}:27017````
* Extract all documents from collection ````flag```` in a readable format:
  * ````db.flag.find().pretty();````



